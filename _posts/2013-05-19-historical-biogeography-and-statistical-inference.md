---
layout: post
title: historical biogeography and statistical inference
date: 2013-05-19 21:42:00
author: Michael Landis
---
Biogeography is the study of the distribution of life throughout time and space. Here we'll describe space in terms of species *ranges*, the shape and area of the geography commonly inhabited by those species. Species ranges rarely remain constant over time, but instead contract, expand, and divide in response to environmental, ecological, and geographical events. We'll focus on historical biogeography, which is chiefly interested in these processes operating over geological timescales. This marriage to geological time is not entirely amicable, because while treating species ranges as functions of time allows us to learn what processes generated biogeographic patterns, time simultaneously complicates the observation of ancestral species ranges we wish to describe (e.g. through taphonomic bias, tectonic drift, etc).

Let's pessimistically assume there's no hope of procuring direct evidence of an ancestral species range (e.g. the complete global fossil record spanning the past six billion years), and instead depend only on data we can reasonably expect to produce for a group of species: the extant species ranges and their shared phylogenetic tree. With a phylogeny in hand and treating the species ranges as random variables, we can model range evolution as a stochastic process and leverage decades of theoretical and computational approaches developed for phylogenetic inference.

Now we can dig into some science equipped with statistical tools. From the likelihood of the extant species ranges, we can assign confidence measures to ancestral species range reconstructions, infer the most likely interval of range evolution parameters (e.g. rate, distance effects), and rule out implausible modes of range evolution via model testing. Of course, biogeography's foibles have introduced its own set of challenges to statistical phylogenetics, which are of primary interest in the posts to come.

---

Additional reading:

Goldberg, E. E., Lancaster, L. T., & Ree, R. H. (2011). Phylogenetic inference of reciprocal effects between geographic range evolution and diversification. *Systematic Biology*, 60(4), 451-465.

Lemey, P., Rambaut, A., Drummond, A. J., & Suchard, M. A. (2009). Bayesian phylogeography finds its roots. *PLoS Computational Biology*, 5(9), e1000520.

Lemmon, A. R., & Lemmon, E. M. (2008). A likelihood framework for estimating phylogeographic history on a continuous landscape. *Systematic Biology*, 57(4), 544-561.

Ree, R. H., Moore, B. R., Webb, C. O., & Donoghue, M. J. (2005). A likelihood framework for inferring the evolution of geographic range on phylogenetic trees. *Evolution*, 59(11), 2299-2311.

Ree, R. H., & Sanmartín, I. (2009). Prospects and challenges for parametric models in historical biogeographical inference. *Journal of Biogeography*, 36(7), 1211-1220.

Ree, R. H., & Smith, S. A. (2008). Maximum likelihood inference of geographic range evolution by dispersal, local extinction, and cladogenesis. *Systematic Biology*, 57(1), 4-14.

Ronquist, F., & Sanmartín, I. (2011). Phylogenetic methods in biogeography. *Annual Review of Ecology, Evolution, and Systematics*, 42, 441-464.

Sanmartín, I., Van Der Mark, P., & Ronquist, F. (2008). Inferring dispersal: a Bayesian approach to phylogeny‐based island biogeography, with special reference to the Canary Islands. *Journal of Biogeography*, 35(3), 428-449.
