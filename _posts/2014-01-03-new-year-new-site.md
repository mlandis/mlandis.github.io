---
layout: default
title: new year, new site 
date: 2014-01-04 13:18:00
author: Michael Landis
---
For the past year, I hosted my research progress on [Google Sites](http://sites.google.com). This is a wonderful free option for hosting cookie-cutter websites. Unfortunately, executing arbitrary Javascript within Google Sites was not permitted for security reasons. Because of this, I never managed to configure Google Sites to properly display syntax-colored code blocks or LaTeX-based equations.

I moved my content to [GitHub Pages](http://pages.github.com) which is compatible with [Jekyll](http://jekyllrb.com)-generated static content. Jekyll supports [MathJax](http://www.mathjax.org/) and [Pygments](http://pygments.org/), enabling LaTeX-rendering and code-syntax-highlighting, respectively.

For example, a Jekyll [Markdown](http://daringfireball.net/projects/markdown/syntax) post containing the code

~~~
$$
L_{l}^{(i)} (s) = \left[ 
        \sum_{s_{j}} \text{Prob} (s_j \mid s, v_j) L_{j}^{(i)}(s_j)
    \right] \times \left[
        \sum_{s_{k}} \text{Prob} (s_k \mid s, v_k) L_{k}^{(i)}(s_k)
    \right]
$$
~~~

with MathJax produces

$$
L_{l}^{(i)} (s) = \left[ 
        \sum_{s_{j}} \text{Prob} (s_j \mid s, v_j) L_{j}^{(i)}(s_j)
    \right] \times \left[
        \sum_{s_{k}} \text{Prob} (s_k \mid s, v_k) L_{k}^{(i)}(s_k)
    \right] 
$$

...and the code

~~~
{{"{% highlight python "}}%}
def f(L,tp,j,k,l):
    for sl,ll in enumerate(L[l]):
        llj = sum([ lj * tp[l,j,sl,sj] for sj,lj in enumerate(L[j]) ])
        llk = sum([ lk * tp[l,k,sl,sk] for sk,lk in enumerate(L[k]) ])
        L[l,sl] = llj * llk
{{"{% endhighlight "}}%}
~~~

with Pygments produces

{% highlight python %}
def f(L,tp,j,k,l):
    for sl,ll in enumerate(L[l]):
        llj = sum([ lj * tp[l,j,sl,sj] for sj,lj in enumerate(L[j]) ])
        llk = sum([ lk * tp[l,k,sl,sk] for sk,lk in enumerate(L[k]) ])
        L[l,sl] = llj * llk
{% endhighlight %}

...and voilà! We have a major component of Felsenstein's pruning algorithm!

With these features working, I'm looking forward to writing practical posts containing code snippets or educational posts dissecting the math we use to model evolution.
