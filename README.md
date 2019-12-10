# Problem Set 2

Due Thursday December 19, 5 p.m., but with an automatic extension if you desire
to Monday Dec 23 (no need to ask).  As with PS1, please submit it by committing
to a shared git repository.

The total achievable for this problem set is 100 points; you will see that there
are four problems each of 50 points, so you need only complete two problems to
earn full credit.

## Problem 1

Cosmology from type Ia supernovae.  In the `datasets` directory you will find a
data set from [Scolnic et al. (2017)](https://arxiv.org/abs/1710.00845) that
records observations of many type Ia supernovae.  The file is called
`hlsp_ps1cosmo_panstarrs_gpc1_all_model_v1_lcparam-full.txt`.  The relevant
columns for this part of the work are the measurement of the redshift in the CMB
rest frame `zcmb`, the observed magnitude of each supernova (standardized based
on various fitting formulae to the shape of the lightcurve) `mb`, and its
associated uncertainty `dmb`.

The observed magnitude is related to the luminosity distance and, through the
cosmological parameters of the Hubble constant, the matter density, and the dark
energy density via standard formulae, the redshift; see, for example, [Hogg
(1999)](https://arxiv.org/abs/astro-ph/9905116).  Following the example in class
that used the relationship between resistance, voltage, and observed current in
a simple circuit, the goal of this problem is to constrain the matter and dark
energy contant of the universe (and to measure its spatial curvature---see Hogg
(1999)).  In this problem, the redshift will play the role of the adjustable
resistor (which we get to set, or measure perfectly for each system); the
observed magnitude will play the role of the measured current; and the formulas
in Hogg (1999) will relate these quantities and the parameters we want to
measure.

1. First, convince yourself that, unless you know the absolute magnitude of Type
Ia SNe, you will be unable to measure the Hubble constant (this is the "distance
ladder" problem).  You will still need to include a parameter for the Hubble
constant (or the equivalent "Hubble distance" in your models; it will just be
degenerate with an offset in `mb`)  (10 points)

1. Write some code that produces the luminosity distance at a given redshift and provided values for `H0`, `Omega_M`, and `Omega_Lambda`.  Don't forget to test it---a good test would be to reproduce Figure 3 of Hogg (1999).  Write the simple function that converts this to the corresponding magnitude.  (20 points).

1. Either by sampling with your own MCMC, by using emcee, or by other methods,
derive the posterior probability for `Omega_M`, `Omega_Lambda`, and `H0` or
`d_H` from this observed data set.  See if you can reproduce Figure 18 of Scolnic, et al. (2017).  (25 points).

1. How spatially flat is the universe (i.e. what is the posterior distribution for `Omega_K = 1 - Omega_M - Omega_Lambda`)?  (5 points).

## Problem 2
