---
layout: default
title: research
---
<h1>Research</h1>

<!--
Due to technological and mathematical reasons, statistical phylogenetic research has largely focused on models of molecular evolution.
Two of the most salient aspects of biodiversity, the morphological and geographical variation of species, have a rich theoretical histories in biology, but lack statistical tools to test longstanding theories.
-->
Models of evolutionary processes help us understand how biodiversity is generated, sustained, and lost.
My primary research interests include **statistical phylogenetics**, **Bayesian inference**, **historical biogeography**, and **phenotypic evolution**.
The Landis Lab studies evolution by developing probabilistic models, writing open source and community-minded software, and analysing simulated and empirical data.
These methods are available as open source software (see below).
We maintain a broad and active interest in phylogenetic inference, and develop for [RevBayes](http://revbayes.com), an open-source package for modeling evolutionary processes and estimating trees.

#### Historical biogeography

Historical biogeography studies the distribution of species in space and time.
Because many species have no known fossil record, biogeographers often rely on reconstructing ancestral species ranges to understand how ranges change over time.
Only recently, parametric models have been used in a phylogenetic context to estimate ancestral species ranges, represented presence-absence states for sets of discrete areas.
Methodologically, we are interested in techniques to allow the models to be applied to high-resolution, global-scale datsets.
For models, we are interested how biogeographic inference may improve phylogenetic estimates.

##### Related work

<table>
    <tr>
        <td markdown="span">
            <img src="../assets/research/img/Landis_et_al_2018_Evolution_silversword_radiation.png" style="float: left; margin:0px 10px 0px 0px" height="100" width="180" class="img-circle-5">
        </td>
        <td markdown="span">
            **Landis, M. J.**, Freyman, W. A., & Baldwin, B. G. (2018). Retracing the silversword radiation despite phylogenetic, biogeographic, and paleogeographic uncertainty. Evolution (Accepted).<br>
            [[paper](../assets/research/pdf/Landis_et_al_2018_bioRxiv_silversword_radiation)]  [[scripts](http://github.com/mlandis/biogeo_silversword)]
        </td>
    </tr>

    <tr>
        <td markdown="span">
            <img src="../assets/research/img/Landis_2016_SystBiol_biogeographic_dating.png" style="float: left; margin:0px 10px 0px 0px" height="100" width="180" class="img-circle-5">
        </td>
        <td markdown="span">
            **Landis, M. J.** (2017). Biogeographic dating of speciation times using paleogeographically informed processes. Systematic Biology, 66(2):128-144.<br>
            [[paper](../assets/research/pdf/Landis_2016_SystBiol_biogeographic_dating.pdf)]  [[scripts](http://github.com/mlandis/biogeographic_dating)]
        </td>
    </tr>

    <tr>
        <td markdown="span">
            <img src="../assets/research/img/Landis_et_al_2013_SystBiol_biogeography_many_areas.png" style="float: left; margin:0px 10px 0px 0px" height="100" width="180" class="img-circle-5">
        </td>
        <td markdown="span">
            **Landis, M. J.**, Matzke, N. J., Moore, B. R., & Huelsenbeck, J. P. (2013). Bayesian Analysis of Biogeography when the Number of Areas is Large. Systematic Biology, 62(6):789-804.<br>
            [[paper](../assets/research/pdf/Landis_et_al_2013_SystBiol_biogeography_many_areas.pdf)]  [[software](http://software.google.com/p/archive/bayarea)]
        </td>
    </tr>

    <tr>
        <td markdown="span">
            <img src="../assets/research/img/Landis_Bedford_2014_Bioinfo_phylowood.png" style="float: left; margin:0px 10px 0px 0px" height="100" width="180" class="img-circle-5">
        </td>
        <td markdown="span">
            **Landis, M. J.** and Bedford, T. (2014). Phylowood: interactive web-based animations of biogeographic and phylogeographic histories. Bioinformatics, 30(1), 123-124.<br>
            [[paper](../assets/research/pdf/Landis_Bedford_2014_Bioinfo_phylowood.pdf)]  [[software](http://mlandis.github.io/phylowood)]
        </td>
    </tr>
</table>

#### Phenotypic evolution

Darwin's original conception of evolution proposed that species evolve gradually over time.
In phylogenetics, this is often modeled as a Brownian motion, whereby small changes occur over many small intervals of time.
Many evolutionary mechanisms, such as rapid adaptation, may produce "pulses" in variation, with punctuated change of large effect.
Rapid change should produce power-law (or heavy-tailed) distributions of traits, but Brownian motion does not generate this feature.
It is difficult to detect these bursts if they are not modeled appropriately.
To search for signals of punctuated evolution, we apply a flexible class of stochastic processes that produce gradual and/or punctuational patterns of change, called Lévy processes.

##### Related work

<table>
    <tr>
        <td markdown="span">
            <img src="../assets/research/img/Landis_Schraiber_2017_PNAS_pulse_vertebrate.png" style="float: left; margin:0px 10px 0px 0px" height="100" width="180" class="img-circle-5">
        </td>
        <td markdown="span">
            **Landis, M. J.** and Schraiber, J. G. (2017). Pulsed evolution shaped modern vertebrate body sizes. Proceedings of the National Academy of Sciences, 114(50) 13224-13229.<br>
            [[paper](../assets/research/pdf/Landis_Schraiber_2017_PNAS_pulse_vertebrate.pdf)]  [[software](http://github.com/Schraiber/pulsR)]
        </td>
    </tr>

    <tr>
        <td markdown="span">
            <img src="../assets/research/img/Schraiber_Landis_2014_TPB_quant_coalescent.png" style="float: left; margin:0px 10px 0px 0px" height="100" width="180" class="img-circle-5">
        </td>
        <td markdown="span">
            Schraiber, J. G. and **Landis, M. J.**. (2015). Sensitivity of quantitative traits to mutational effects and number of loci. Theoretical population biology, 102: 85-93.<br>
            [[paper](../assets/research/pdf/Schraiber_Landis_2014_TPB_quant_coalescent.pdf)]  [[scripts](http://github.com/Schraiber/quant_trait_coalescent)]
        </td>
    </tr>

    <tr>
        <td markdown="span">
            <img src="../assets/research/img/Landis_et_al_2012_SystBiol_phylo_levy.png" style="float: left; margin:0px 10px 0px 0px" height="100" width="180" class="img-circle-5">
        </td>
        <td markdown="span">
            **Landis, M. J.** (\*), Schraiber, J. G. (\*), & Liang, M. (2013). Phylogenetic Analysis Using Lévy Processes: Finding Jumps in the Evolution of Continuous Traits. Systematic Biology, 62(2):193-204.<br>
            [[paper](../assets/research/pdf/Landis_et_al_2012_SystBiol_phylo_levy.pdf)]  [[software](http://github.com/mlandis/creepy-jerk)]
        </td>
    </tr>
</table>


(\*) - Lead co-authors.

#### Phylogenetic inference with RevBayes

Learning the degree of relatedness between species has far-reaching implications for biological research, from basic research questions in evolution and ecology, to applied questions in medical research, epidemiology, forensics, and biodiversity management.
Estimating a phylogeny, of course, depends on one's model assumptions, which vary depending on the nature of the study.
[RevBayes](http://revbayes.com) was designed to allow researchers to tailor models to their needs.
RevBayes achieves this by providing a flexible scripting language to describe probabilistic graphical models.

##### Related work

<table>
    <tr>
        <td markdown="span">
            <img src="../assets/research/img/Hoehna_et_al_2017_Bioinformatics_parallel_marg_like.png" style="float: left; margin:0px 10px 0px 0px" height="100" width="180" class="img-circle-5">
        </td>
        <td markdown="span">
            Höhna, S., **Landis, M. J.**, and  B. R., Huelsenbeck. (2017).  Parallel power posterior analyses for fast computation of marginal likelihoods in phylogenetics. Bioinformatics, Accepted.
<br>[[paper (pre-print)](../assets/research/pdf/Hoehna_et_al_2017_bioRxiv_parallel_marg_like.pdf)]
        </td>
    </tr>

    <tr>
        <td markdown="span">
            <img src="../assets/research/img/Hoehna_et_al_2017_CurrProcBioinfo_revbayes.png" style="float: left; margin:0px 10px 0px 0px" height="100" width="180" class="img-circle-5">
        </td>
        <td markdown="span">
            Höhna, S., **Landis, M. J.**, and Heath, T. A. (2017). Phylogenetic Inference Using RevBayes. Current Protocols in Bioinformatics, 57:6.16-6.16.34.
<br>[[paper](../assets/research/pdf/Hoehna_et_al_2017_CurrProcBioinfo_revbayes.pdf)]
        </td>
    </tr>

    <tr>
        <td markdown="span">
            <img src="../assets/research/img/Hoehna_et_al_2016_SystBiol_revbayes.png" style="float: left; margin:0px 10px 0px 0px" height="100" width="180" class="img-circle-5">
        </td>
        <td markdown="span">
            Höhna, S., **Landis, M. J.**, Heath, T. A., Boussau, B., Lartillot, N., Moore, B. R., Huelsenbeck, J. P. & Ronquist, F. (2016). RevBayes: Bayesian Phylogenetic Inference Using Graphical Models and an Interactive Model-Specification Language. Systematic Biology, 65(4):726-736.
<br>[[paper](../assets/research/pdf/Hoehna_et_al_2016_SystBiol_revbayes.pdf)]  [[software](http://github.com/revbayes/revbayes)]
        </td>
    </tr>

    <tr>
        <td markdown="span">
            <img src="../assets/research/img/Hoehna_et_al_2014_SystBiol_graphical_models.png" style="float: left; margin:0px 10px 0px 0px" height="100" width="180" class="img-circle-5">
        </td>
        <td markdown="span">
            Höhna, S., Heath, T. A., Boussau, B., **Landis, M. J.**, Ronquist, F., & Huelsenbeck, J. P. (2014). Probabilistic graphical model representation in phylogenetics. Systematic Biology, 63(5):753-771.
<br>[[paper](../assets/research/pdf/Hoehna_et_al_2014_SystBiol_graphical_models.pdf)]
        </td>
    </tr>
</table>
