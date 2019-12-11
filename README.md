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

Spin is a fundamental property of a Kerr black hole.  Advanced LIGO does not
measure the spins of black holes in merging binary black hole systems
particularly well, but it does measure one (scalar) combination of spins well.
This parameter is called the effective spin (`chi_eff`) of the black hole, and
is a mass-weighted combination of the component of each black hole's angular
momentum vector projected onto the orbital plane.  See [Farr, et al.
(2017)](https://arxiv.org/abs/1706.01385), for example.  Black holes observed by
other methods, in X-Ray binaries, for example, are thought to often be highly
spinning; in contrast, LIGO has generally measured *small* effective spins for
the 10 binary black hole mergers it has seen to date.

This problem asks you to determine the typical (mean) and scatter (standard
deviation) of the *population* of binary black holes seen by LIGO.  You will do
this by analogy to the "eight-schools" problem discussed in class (where the
goal was to determine the mean and scatter of the test scores across schools).
To a reasonable approximation (but see [Ng, et al.
(2018)](https://arxiv.org/abs/1805.03046)), the measurements of `chi_eff` made
by LIGO for each merging BBH system can be treated as a Gaussian; the file
`datasets/GWTC-1-chi_eff.txt` gives the observed mean and standard deviation for
`chi_eff` in each of the 10 BBHs observed by [Abbott, et al.
(2019)](https://arxiv.org/abs/1811.12940).

1. Plot the measured `chi_eff` and uncertainty for the ten events (your choice of how).  What is the weighted mean of the effective spins for the ten events?  Are all events consistent with having exactly this spin value?  Are all events consistent with `chi_eff == 0`?  (15 points).

1. Fit a Gaussian population distribution to this data set, as we did for the eight schools.  Show the joint constraint on the mean and standard deviation of this Gaussian.  Are these results consistent with the answers to part 1?  Compare your results to [Roulet & Zaldarriaga (2019)](https://arxiv.org/abs/1806.10610), Figure 4.  (25 points).

1. Propose a way to quantify how *symmetric* the population of spins is about
`chi_eff == 0`, and apply it to this data set.  Symmetry about `chi_eff == 0`
would be a natural consequence of black hole binaries that form *dynamically* as
opposed to forming out of a pre-existing stellar binary, where the stars can
interact before they become black holes.  Is this catalog of mergers consistent with a dynamical formation history?  (10 points)

## Problem 3

The 1D [non-linear Schrodinger equation](https://en.wikipedia.org/wiki/Nonlinear_Schr%C3%B6dinger_equation) describes the propagation of light through a non-linear medium.  Note that the solution we are seeking, `psi`, is complex.  For `kappa < 0`, there are "focusing" solutions that have spatially-localized propagating wave packets.  Let `kappa = -0.1` in this problem.  

1. Write down a finite-difference form of the NLS, with spacing in time `dt` and space `dx`; as we did with the linear diffusion equation, symmetrize the evaluation of the spatial part of the equation in time.  (10 points)

1. Assume we are *near* a solution at the advanced time, and write down the finite difference equation for the error term `e` at the advanced time in `psi_new = psi - e`, assuming that `e` is small enough that any term of order `e^2` or higher can be neglected.  (You can either work directly from the finite-difference equations of the previous part, or write first the linearized continuous PDE, and then discretize that).  (10 points)  

1. Write a multigrid solver that will find the solution for the error term at the advanced time assuming periodic boundary conditions.  (20 points).

1. Apply your multigrid solver as part of a time-stepping routine for solving the NLS on a spatial domain $0 < x < 1$ with periodic boundary conditions and a (purely real) Gaussian initial condition with a small (you choose) width.  Show the evolution of the solution with time, in both amplitude and phase; do you see focusing? (10 points).
