---
layout: post
title: summer updates
date: 2013-06-02 13:29:00
author: Michael Landis
---
Evolution 2013 was very enjoyable, though exhausting (my classmates and I carpooled and camped). To share some of my "paperless" research, such as my Evolution talk, I created a [Figshare](http://figshare.com/authors/Michael%20Landis/427371) account.

I received some great feedback about [BayArea](http://code.google.com/p/bayarea) at the conference, both from empiricists and theorists. Designing new models is the next part, which is driving force behind increasing the number of areas per analysis. As an aside, I updated BayArea to fix a problem for proposing histories for small numbers of areas (N < 10). Thanks to Julien Vieu for mentioning the problem.

Also, I updated [creepy-jerk](http://github.com/mlandis/creepy-jerk) (continuous character evolution using Lévy processes) to improve performance for computing the compound Poisson process with normally distributed jumps. While doing this, I modified the code to produce a FigTree-compatible output file that indicates the size and polarity of jumps on the phylogeny (using the posterior of sampled jumps and the signal-to-noise ratio divided by the square root of the branch length).

<a href="/assets/cj_eg_fig.png"><img src="/assets/cj_eg_fig.png" alt="creepy-jerk posterior jumps" style="width: 500px" align="center"/></a>

Looks nice, I think!
