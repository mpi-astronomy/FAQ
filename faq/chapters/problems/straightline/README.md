---
title: How to fit a straight line?
authors:
- name: Morgan Fouesneau
  orcid: 0000-0001-9256-5516
  affiliation: mpia
affiliations:
    - id: mpia
      institution: Max Planck Institute for Astronomy, Königstuhl 17, 69117 Heidelberg, Germany 
      ror: https://ror.org/01vhnrs90
      isni: 0000 0004 0491 677X
      department: Data Science Department
      address: Königstuhl 17
      city: Heidelberg
      country: Germany
      postal_code: 69117
date: 2018-08-10
---

# Introduction

In astronomy, we commonly have to fit a model to data. A very typical example is the fit of a straight line to a set of points in a two-dimensional plane.  Astronomers are very good at finding a representation or a transformation of their data in which they can identify linear correlations (e.g., plotting in log-log space, action angles for orbits, etc).  Consequently, a polynomial remains a "line" in a more complicated representation space.

In this exercise, we consider a dataset with uncertainties along one axis only for simplicity, i.e. uncertainties along x negligible. These conditions are rarely met in practice but the principles remain similar.
However, we also explore the outlier problem: bad data are very common in astronomy.

We emphasize the importance of having a "generative model" for the data, even an approximate one.
Once there is a generative model, we have a direct computation of the likelihood of the parameters or the posterior probability distribution.

We explore solutions with various common frameworks

:::::{grid} 1 2 3 4

::::{card}
:url: /straighlinefit-emcee
Emcee
::::
::::{card}
:url: /straighlinefit-jax
Numpyro + JAX
::::
::::{card}
:url: /straighlinefit-pymc3
PyMC3
::::
::::{card}
:url: /straighlinefit-pystan
PyStan
::::

:::::
