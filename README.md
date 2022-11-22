# Bioinformatic Tools

Here we list number of packages that are useful for different aspects of the data analysis process for bioinformatics datasets.

## Table of Contents

## Differential abundance testing

* **[MaAsLin2](https://huttenhower.sph.harvard.edu/maaslin/)**: a package for efficiently determining multivariable association between phenotypes, environments, exposures, covariates and microbial meta’omic features. MaAsLin2 relies on general linear models to accommodate most modern epidemiological study designs, including cross-sectional and longitudinal, and offers a variety of data exploration, normalization, and transformation methods. This tool was specifically designed for use with microbiome data, but can be influenced heavily by outliers.
* **[LIMMA](https://kasperdanielhansen.github.io/genbioconductor/html/limma.html)**: LIMMA stands for "linear models for microarray data". Although originally developed for RNAseq microarray data, it is also particularly good at identifying differential abundance in normalised microbiome and metabolomics/lipidomics datasets. We also provide a convenient wrapper around this function for phyloseq objects (called `phyloseq_limma`) [here](https://github.com/mucosal-immunology-lab/microbiome-analysis).

## Data modelling

### Model selection

Often we will be interested in testing multiple models to determine which offers the best fit, maximising the total variance explained while minimising the risk of overfitting. Common metrics of these are [Akaike's Information Criterion](https://en.wikipedia.org/wiki/Akaike_information_criterion) (AIC or AICc for low sample size), [Bayesian Information Criterion](https://en.wikipedia.org/wiki/Bayesian_information_criterion) (BIC), and [Deviance Information Criterion](https://en.wikipedia.org/wiki/Deviance_information_criterion) (DIC; especially useful for model posterior distributions have been obtained by Markov Chain Monte Carlo (MCMC) simulation). One explanation of the differences in metrics can be viewed [here](https://studystics1.medium.com/odyssey-of-a-data-scientist-information-criteria-aic-bic-dic-waic-both-r-and-python-code-d11a4ac1c0be).

* **[MuMIn](https://rdrr.io/cran/MuMIn/man/MuMIn-package.html)**: MuMIn stands for "multi-model inference". This package offers functions to streamline the information-theoretical model selection process and carry out model averaging based on information criteria. A particularly useful element is the [`dredge`](https://rdrr.io/cran/MuMIn/man/dredge.html) function, which generates a model selection table with combinations (subsets) of fixed effect terms in a global model, with optimal model inclusion rules (can use multiple metrics to choose the best model, such as AIC, AICc, BIC etc.). This is particularly useful when determining which elements to retain for your models. It works with a range of [fitted models](https://rdrr.io/cran/MuMIn/man/supported-classes.html), but requires a work-around for models that don't store the model call in their outputs (via a wrapper function created by [`updateable`](https://rdrr.io/cran/MuMIn/man/updateable.html)).

### Linear mixed effect models

These models, abbreviated as LMM models, offer an extension to simple linear models and allow both fixed and random effects. They are particularly useful when there is non-independence in the data, such that there is some hierarchical structure to the data. For example, mice could be considered per cage, or individual patients in a longitudinal study where multiple samples are collected from the same individual over time (they act as their own control group).

* **[lmerTest](https://rdrr.io/cran/lmerTest/man/lmerTest-package.html)**: The lmerTest package extends the [lme4](https://rdrr.io/cran/lme4/) package, and provides p-values in type I, II or III anova and summary tables for linear mixed models (lmer model fits via lme4) via Satterthwaite's degrees of freedom method; a Kenward-Roger method is also available via the pbkrtest package. Model selection and assessment methods include step, drop1, anova-like tables for random effects (ranova), least-square means (LS-means; ls_means) and tests of linear contrasts of fixed effects (contest). 

* **[MCMCglmm](https://www.rdocumentation.org/packages/MCMCglmm)**: This package offers a Bayesian approach to fitting Multivariate Generalised Linear Mixed Models (and related models) using Markov chain Monte Carlo techniques. Some tutorials for this package can be found here: 
  * Course notes from the package author ([here](https://mran.microsoft.com/snapshot/2018-08-24/web/packages/MCMCglmm/vignettes/CourseNotes.pdf)).
  * Intro to the MCMCglmm package for biologists ([here](https://ourcodingclub.github.io/tutorials/mcmcglmm/)).

## Data visualisation

* **[volcano3D](https://rdrr.io/cran/volcano3D/)**: Generates interactive plots for analysing and visualising three-class high dimensional data - it is particularly suited to visualising differences in continuous attributes such as gene/protein/biomarker expression levels between three groups. It can produce 3-way polar plots for easier interpretation of three-class data following prior differential abundance analysis testing (example below). An example of a 2x3 study design (responders and non-responders to 3 distinct drugs) is provided [here](https://katrionagoldmann.github.io/volcano3D/articles/Vignette_2x3.html).<br><div align="center"><img src="./assets/volcano3d_polarplot.png" width=60%></div>

## Machine learning