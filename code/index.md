---
layout: default
title: code
---

#### [BayArea](http://code.google.com/p/bayarea/) ####
---


BayArea infers the posterior distribution of ancestral ranges of extant species when supplied their observed ranges and time-calibrated phylogeny. Range evolution is modeled on the phylogeny as a continuous-time Markov process, much as it is for molecular evolution, with ranges being binary presence-absence vectors corresponding to discrete geographical areas. This method ideal for data spanning many areas (more than 10) and quantifying uncertainty in ancestral range reconstructions.

[Source code](http://code.google.com/p/bayarea/) is written in C++. Manuscript figures were produced using [BayArea-Fig](http://mlandis.github.io/bayarea-fig/) and is written in Javascript.

Described in

> Landis, M. J., Matzke, N. J., Moore, B. R., & Huelsenbeck, J. P. (2013). Bayesian analysis of biogeography when the number of areas is large. *Systematic Biology*, 62(6), 789–804. doi:10.1093/sysbio/syt040.

#### [Phylowood](http://mlandis.github.io/phylowood/) ####
---

Phylowood allows users to efficiently explore phylogeographic range reconstructions via temporal, geographical, and phylogenetic filters. This tool runs in any modern web browser without requiring software installation. This was written as part of [Google Summer of Code 2012](http://informatics.nescent.org/wiki/Phyloinformatics_Summer_of_Code_2012#Phylowood.js:_Browser-based_Interactive_Animations_of_Ancestral_Dispersal_and_Diversity_Patterns).

[Source code](http://mlandis.github.io/phylowood) is written in Javascript, relying heavily on [D3](http://d3js.org/).

Described in 

> Landis, M. J., & Bedford, T. (2013). Phylowood: interactive web-based animations of biogeographic and phylogeographic histories. *Bioinformatics*, 30(1), 123–124. doi:10.1093/bioinformatics/btt635

#### [creepy-jerk](http://github.com/mlandis/creepy-jerk/) ####
---

Lévy processes are an expressive class of stochastic processes that produce discontinuous sample paths containing "jumps". Provided continuous trait values and a time-calibrated phylogeny, creepy-jerk infers the evolutionary process parameters and the placement and size of jumps of trait values over the tree. creepy-jerk currently supports the $$\alpha$$-stable process, the compound Poisson process with normally distributed jumps, and the variance gamma process.

[Source code](http://github.com/mlandis/creepy-jerk) is written in C++, and produces [FigTree](http://tree.bio.ed.ac.uk/software/figtree/)-compatible output to visualize the posterior distribution of jumps.

Described in

> Landis, M. J.\*, Schraiber, J. G.\*, & Liang, M. (2013). Phylogenetic analysis using Lévy processes: finding jumps in the evolution of continuous traits. *Systematic Biology*, 62(2), 193–204. doi:10.1093/sysbio/sys086

#### [RevBayes](http://sourceforge.net/projects/revbayes/) ####
---

An R-like environment and C++ library for the evolutinary analysis of graphical models using Bayesian inference.

( under development )
