# Straightline fitting problem

In astronomy, we commonly have to fit a model to data. A very typical example is the fit of a straight line to a set of points in a two-dimensional plane.  Astronomers are very good at finding a representation or a transformation of their data in which they can identify linear correlations (e.g., plotting in log-log space, action angles for orbits, etc).  Consequently, a polynomial remains a "line" in a more complicated representation space.

In this exercise, we consider a dataset with uncertainties along one axis only for simplicity, i.e. uncertainties along x negligible. These conditions are rarely met in practice but the principles remain similar.
However, we also explore the outlier problem: bad data are very common in astronomy.

We emphasize the importance of having a "generative model" for the data, even an approximate one.
Once there is a generative model, we have a direct computation of the likelihood of the parameters or the posterior probability distribution.

We explore solutions with various common frameworks

* `emcee`
[![nbviewer](https://raw.githubusercontent.com/jupyter/design/master/logos/Badges/nbviewer_badge.svg)](https://nbviewer.org/github/mpi-astronomy/FAQ/blob/main/coding/straightline/straighlinefit_emcee.ipynb)
[![Binder](https://mybinder.org/badge.svg)](https://mybinder.org/v2/gh/mpi-astronomy/FAQ/blob/main/coding/straightline/straighlinefit_emcee.ipynb)
* `PyMC3`
[![nbviewer](https://raw.githubusercontent.com/jupyter/design/master/logos/Badges/nbviewer_badge.svg)](https://nbviewer.org/github/mpi-astronomy/FAQ/blob/main/coding/straightline/straighlinefit_pymc3.ipynb)
[![Binder](https://mybinder.org/badge.svg)](https://mybinder.org/v2/gh/mpi-astronomy/FAQ/blob/main/coding/straightline/straighlinefit_pymc3.ipynb)
* `pyStan`,
[![nbviewer](https://raw.githubusercontent.com/jupyter/design/master/logos/Badges/nbviewer_badge.svg)](https://nbviewer.org/github/mpi-astronomy/FAQ/blob/main/coding/straightline/straighlinefit_pystan.ipynb)
[![Binder](https://mybinder.org/badge.svg)](https://mybinder.org/v2/gh/mpi-astronomy/FAQ/blob/main/coding/straightline/straighlinefit_pystan.ipynb)
* and `jax + numpyro`
[![nbviewer](https://raw.githubusercontent.com/jupyter/design/master/logos/Badges/nbviewer_badge.svg)](https://nbviewer.org/github/mpi-astronomy/FAQ/blob/main/coding/straightline/straighlinefit_jax.ipynb)
[![Binder](https://mybinder.org/badge.svg)](https://mybinder.org/v2/gh/mpi-astronomy/FAQ/blob/main/coding/straightline/straighlinefit_jax.ipynb)
