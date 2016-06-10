---
layout: post
title: graphical models in RevBayes
date: 2016-05-16 13:16:00
author: Michael Landis
---

*This post is part of a [series](2016/01/27/revbayes-overview.html) exploring features in [RevBayes](http://revbayes.com).* 

You bet heads on the coin flip, and lose again.
Your host wonders aloud what the chances of losing five games in a row might be.
Most would reply the odds for heads over tails is fifty-fifty, which comes to $$2^{-5}$$ for five trials, assuming a fair coin.
But, then again, the hour is late, the carnival is closed, and your host with the pointed mustache pours you more wine.
You begin to question whether it is a fair coin.

This is to ask how are the data distributed for what parameters.
A coin flip may be represented as a random variable, $$H$$, which can either be heads, $$H=1$$, or tails, $$H=0$$.
The [Bernoulli distribution](https://en.wikipedia.org/wiki/Bernoulli_distribution) says a random variable takes the value $$1$$ with probability $$p$$.
That is, $$p$$ is a parameter that controls how fair the coin is.
Mathematically, $$H \sim \text{Bernoulli} \left( 0.5 \right)$$ states that the value of $$H$$ is distributed by a Bernoulli distribution, where $$H=0$$ and $$H=1$$ each occur with probability $$p=(1-p)=0.5$$.
The naive and trusting model, $$M_0$$, is programmed in RevBayes like so

{% highlight R %}
> # M0: the mark's coin-flipping model
> h ~ dnBernoulli(p=0.5)
> h.clamp(1)
> h.probability()
   0.5
{% endhighlight %}

Alternatively, a model anticipating a con game, $$M_1$$, seeks to represent that the fairness of the coin is unknown, but biased towards flipping tails (i.e. $$p < 0.5$$ is expected).
is $$p=q^2$$, where $$q$$ might take on any possible amount of unfairness, $$0 \leq q \leq 1$$.
This is described mathematically with the three statements, $$H \sim \text{Bernoulli} \left( p \right)$$, $$q \sim \text{Uniform} \left( 0.0, 1.0 \right)$$, and $$p = q^2$$. 
The corresponding RevBayes code for $$M_1$$ is

{% highlight R %}
> # M1: the grifter's coin-flipping model
> lower <- 0.0
> upper <- 0.1
> q ~ dnUniform(lower, upper)
> p := q^2 
> h ~ dnBernoulli(p)
>
> # Assume a heads is flipped
> h.clamp(1)
> 
> # What is the likelihood if p==0.25 (q=0.5)?
> q.setValue(0.5)
> h.probability()
   0.25
>
> # What if p==0.01 (q=0.1)?
> q.setValue(0.1)
> h.probability()
   0.01
{% endhighlight %}

In the example for $$M_1$$, we see that the probability the coin is heads, `h`, depends on the value of `p`.
`p` itself depends on the value of `q`, which, in turn, is drawn from a uniform distribution with bounds imposed by `lower` and `upper`.

#### Probabilistic graphical models

A pattern is emerging where model complexity grows in response to the number of parameters and the dependencies among those variables.
When a model has very few variables, like with our coin-flipping example, these parameter interactions are easy to summarize.
The dependencies between all random variables in the model can be written explicitly in terms of equations.
For large and complex models, like phylogenetic models, the incredible number of parameter interactions can be overwhelming.

<img src="assets/graphical_model.png" alt="Graphical model" align="right" style="width:350px;margin: 20px 0px 20px 20px;"/>

Any model with a strong and separable dependency structure may be equivalently represented as a [probabilistic graphical model](https://en.wikipedia.org/wiki/Graphical_model), and visualized as a [directed acyclic graph](https://en.wikipedia.org/wiki/Directed_acyclic_graph).
RevBayes fundamentally treats models as probabilistic graphs, a perspective that offers several advantages.
First, it offers a power visualization tool, useful both for summarizing and reducing model complexity, and for teaching.
The dependency structure lends itself to various computational efficiencies, including marginalization techniques, Markov chain Monte Carlo, generative simulations.
Graphs also modular, in that they can be decomposed into subgraphs while retaining their internal topologies.
This is improves code design and reusability both when specifying models using the Rev language, and when developing the back-end architecture powering RevBayes.
These sentiments are summarized in [Hoehna et al. (2014)](http://sysbio.oxfordjournals.org/content/63/5/753.full) and will be reinforced throughout this series of posts.

A brief overview of specifying graphical models in RevBayes is given below.

#### Constant nodes: solid squares

A model variable that is known is a *constant node*.
Constant nodes are treated as known variables and are not estimated during inference.
Creating a constant node is done using the `<-` assignment operator.

{% highlight R %}
> p <- 0.5
> p
   0.5
{% endhighlight %}

#### Stochastic nodes: solid circles

Probabilistic inference is primarily interested in learning the values of the unknown parameters that summarize the data.
Each of these parameters is a *stochastic node*.
Stochastic nodes are created using the `~` operator, where the right-hand side gives the distribution (and parameters) that measure the probability of the random variable on the left-hand side.

{% highlight R %}
> p <- 0.5
> h ~ dnBernoulli(p)
>
> # h is initialized with a random value
> h
    0
> h.probability()
    0.5
{% endhighlight %}


RevBayes works with [generative models](https://en.wikipedia.org/wiki/Generative_model), which allows for an exact match between the simulation model and the inference model.
This greatly simplifies workflows involving simulation analyses, such as model validation and statistical power analyses.

#### Deterministic nodes: dotted circles

A variable whose value is exactly determined by other model variables is a *deterministic node*.
Deterministic nodes have a value equal to a function of any number and combination of constant, deterministic, and stochastic nodes, which is defined using the `:=` operator.
This affords great flexibility in parameterizing the model.

{% highlight R %}
> q <- 0.5
> p := q^2
> p
   0.25
{% endhighlight %}

Deterministic nodes are immediately updated when any of their parental nodes' values are changed.

{% highlight R %}
> q <- 0.4
> p 
   0.16
{% endhighlight %}

The probability of a stochastic node changes whenever its distribution's parameters change.

{% highlight R %}
> q <- 0.5
> p := q^2
> h ~ dnBernoulli(p)
> h.probability()
   0.25
> q <- 0.4
> h.probability()
   0.16
{% endhighlight %}

#### Observed (stochastic) nodes: shaded circles

During inference, some random variables are *observed* to have particular values.
For example, an individual coin (the variable) might show heads or tails (the values) after being flipped.
Once the coin is observed to be, say, tails ($$H=0$$), the question of interest becomes what is the likelihood that the coin flip resulted in tails under its distribution.
That is, the unobserved random variable might take any number of values, but the observed random variable is "clamped" to the actual value of the trial.
To clamp a stochastic node to be observed for some value

{% highlight R %}
> q <- 0.5
> p := q^2
> h ~ dnBernoulli(p)
> obs <- 0
> h.clamp(obs)
> h.probability()
    0.75
{% endhighlight %}

In effect, calling `clamp` sets the node's value and distinguishes it to be included in the model likelihood (rather than part of the prior).
Future posts will discuss how this distinction affects certain parts of Bayesian analyses, such as computing [Bayes factors](https://en.wikipedia.org/wiki/Bayes_factor).


#### Plates (replicated subgraphs)

Models often contain repetitive structures, which may be represented compactly.
Graphical models use [plates](https://en.wikipedia.org/wiki/Plate_notation).
In RevBayes `for` loops are the simplest way to represent.

{% highlight R %}
> p <- 0.25
> for (i in 1:100) {
+     x[i] ~ dnBernoulli(p)
+ }
> x_mean := mean(x)
> x_mean
    0.22
{% endhighlight %}

They are also useful for succinctly imposing a [Markov property](https://en.wikipedia.org/wiki/Markov_property) between model variables.

{% highlight R %}
> x[1] ~ dnNormal(mean=0, sd=1)
> dx[1] <- 0.0
> for (i in 2:10) {
+     x[i] ~ dnNormal(mean=x[i-1], sd=1)
+     dx[i] := x[i] - x[i-1]
+ }
> z
   [ 0.596103, 0.291775, 1.02862, -0.0848241, -3.08975,
     -2.90331, -3.41427, -4.46115, -5.62696, -6.33428 ]
> dz
   [ 0, -0.304328, 0.736843, -1.11344, -3.00493, 
     0.186437, -0.510954, -1.04688, -1.16581, -0.707318 ]
{% endhighlight %}

#### Parent-child relationships

The `structure` (or `str`) function is useful to learn about how the nodes relate to one another. For example, the node `q` is the parent of `p` and the child of `lower` and `upper`.

{% highlight R %}
> lower <- 0.0
> upper <- 1.0
> q ~ dnUniform(lower, upper)
> p := q^2
> structure(q)

   _variable     = q
   _dagType      = Stochastic DAG node
   _clamped      = FALSE
   _lnProb       = 0
   _parents      = [ lower, upper ]
   _children     = [ p ]
{% endhighlight %}

Assigning a new value to `p` will cause `q` to lose `p` as a child.

{% highlight R %}
> p <- 5.0
> structure(q)

   _variable     = q
   _dagType      = Stochastic DAG node
   _clamped      = FALSE
   _lnProb       = 0
   _parents      = [ lower, upper ]
   _children     = [ p ]
{% endhighlight %}

#### Wrapping up

Of course, phylogenetic models are more complex than coin flipping experiments.
The basic building blocks to compose richer models are essentially the same.
That's the beauty of graphical models: that simple relationships can generate scalable complexity.
In the long run, the goal is not only to build models that formalize our understanding of nature, but to learn about the behavior of the processes that generate biodiversity.

Next time we'll look into RevBayes data structures.
