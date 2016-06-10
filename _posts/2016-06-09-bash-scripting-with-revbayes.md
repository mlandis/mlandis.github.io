---
layout: post
title: bash scripting with RevBayes
date: 2016-06-09 22:19:30
author: Michael Landis
---

Whether working on genomic datasets or conducting a simulation study, research projects often require identical or nearly identical jobs to be replicated across vast numbers of datasets.
The front-end of [RevBayes](http://revbayes.com) is an interpretted language, which provides users with an agile and powerful interface for scripting.

Let's set up a little scenario to make it easy on the imagination.
Suppose your task is to assess the sensitivity of posterior tree probabilities for one simple and one complex model---say, a Jukes-Cantor model, where all transition rates are equal, and the Felsenstein 81 model, where base frequencies are free parameters to be estimated.
You've stored multiple sequence alignments for all the genes of interest in the folder `genes` in NEXUS format.
You want to use RevBayes to estimate the posterior density for each gene, once assuming the rate matrix is `fnJC` and a second time assuming it is `fnF81`.
Instead of repeatedly modifying and running your RevBayes script, `rb_gene_model.Rev`, you can automate the job in bash using the `echo` command and pipes (`|`).

To follow along or download the scripts, issue these commands in the shell.
{% highlight bash %}
> git clone https://github.com/mlandis/revbayes_bash_scripts.git
> cd batch_job
{% endhighlight %}

First, we'll create a RevBayes script called `rb_gene_model.Rev` that expects three pre-defined variables: `data_file` gives the name of the gene alignment, `job_id` gives the analysis an identity that matches the filename, and `type_Q` gives the type of rate matrix to use.

{% highlight bash %}
# print errors for undefined variables
if (!exists("data_file")) "ERROR: `data_file` undefined"
if (!exists("type_Q"))    "ERROR: `type_Q` undefined"
if (!exists("job_id"))    "ERROR: `job_id` undefined"

# settings
out_prefix = job_id + ".Q_" + type_Q 
out_fp = "output/"

# move/monitor vector indices
mni = 1
mvi = 1

# read data
data = readDiscreteCharacterData(data_file)
taxa = data.taxa()

# define tree model
tree ~ dnBDP(lambda=1, mu=0, rootAge=1, taxa=taxa)
mv[mvi++] = mvNNI(tree, weight=taxa.size())
mv[mvi++] = mvNodeTimeSlideUniform(tree, weight=taxa.size())

# define clock model
clock ~ dnExp(10)
mv[mvi++] = mvScale(clock, weight=2)

# define rate matrix based on value of type_Q
if (type_Q=="JC") {
    Q <- fnJC(4)
} else if (type_Q=="F81") {
    bf ~ dnDirichlet([1,1,1,1])
    mv[mvi++] = mvSimplexElementScale(bf, weight=2)
    Q := fnF81(bf)
}

# create phylogenetic model distribution
seq ~ dnPhyloCTMC(tree=tree,
                  Q=Q,
                  branchRates=clock,
                  nSites=data.nchar(),
                  type="DNA")

# attach the data
seq.clamp(data)

# make the model
mdl = model(seq)

# add monitors
mn[mni++] = mnScreen(clock, printgen=100)
mn[mni++] = mnFile(tree, filename=out_fp+out_prefix+".tre", printgen=100)
mn[mni++] = mnModel(filename=out_fp+out_prefix+".params.log", printgen=100)

# construct MCMC
ch = mcmc(model=mdl, moves=mv, monitors=mn)

# burn-in then run the analysis
ch.burnin(5000, 100)
ch.run(10000)

# quit upon completion
quit()
{% endhighlight %}

Next we'll create a bash script called `rb_gene_job.sh`.
When called, RevBayes treats arguments as files to be sourced, which means we can pipe (`|`) the stdout file from `echo` as a source file into RevBayes.
Perfect for scripting!

{% highlight bash %}
#!/bin/bash

# arg1, input filename
file=$1

# arg2, stripped filename
id=$2

# arg3, rate matrix type
type_Q=$3

# construct the command string
rb_command="data_file = \"$file\";
            job_id = \"$id\";
            type_Q = \"$type_Q\";
            source(\"rb_gene_model.Rev\");"

# pipe the command into RevBayes
echo $rb_command | rb
{% endhighlight %}

Third, we'll create `rb_gene_batch.sh` to repeatedly call `rb_gene_job.sh` with different combinations of arguments.
Note that `debug=0` by default, which will cause RevBayes to be run in the background (`&`) and without being hung up upon closing the terminal (`nohup`).
These are useful features when running jobs on clusters.

{% highlight bash %}
#!/bin/bash
debug=0

# accepts a file list, e.g. "*.nex"
filelist=$@

# model list must match .Rev script
models=("JC" "F81")

# call `rb_gene_job.sh` for each file
for file in $filelist; do
    for m in ${models[@]}; do
        echo "Running model \"$m\" for \"$file\""
        id=$(basename ${file%%.*})
        if [ $debug == 0 ] ; then
            # run all jobs without stdout
            nohup ./rb_gene_job.sh $file $id $m &>/dev/null &
        else 
            # run serial jobs with stdout
            ./rb_gene_job.sh $file $id $m
        fi
    done
done
echo "...done!"
{% endhighlight %}

Everything is in place, and we can run the script.
{% highlight bash %}
> chmod +x *.sh
> ./rb_gene_batch.sh genes/*.nex
Running model "JC" for "genes/primates_cox2.nex"
Running model "F81" for "genes/primates_cox2.nex"
Running model "JC" for "genes/primates_cytb.nex"
Running model "F81" for "genes/primates_cytb.nex"
...done!
{% endhighlight %}
...and in time, the results will appear in the `output` directory.
{% highlight bash %}
> ls -1 output
primates_cox2.Q_F81.params.log
primates_cox2.Q_F81.tre
primates_cox2.Q_JC.params.log
primates_cox2.Q_JC.tre
primates_cytb.Q_F81.params.log
primates_cytb.Q_F81.tre
primates_cytb.Q_JC.params.log
primates_cytb.Q_JC.tre
{% endhighlight %}

That's it!
