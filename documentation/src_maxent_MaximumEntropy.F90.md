# Overview

This file src/maxent/MaximumEntropy.F90 contains...
This Fortran module, `MMaximumEntropy`, implements the Maximum Entropy method for analytic continuation of quantum Monte Carlo data. The core idea is to find the most probable real-frequency spectral function `A(w)` given imaginary-time or Matsubara-frequency Green's function data `G`, and a prior model `m(w)`, by maximizing the posterior probability `Pr(A|G) ~ Pr(G|A) * Pr(A)`. `Pr(G|A)` is the likelihood function (related to chi-squared), and `Pr(A)` is the prior probability, which includes an entropy term `S`. The algorithm iteratively adjusts the spectral function `A(w)` and a Bayesian parameter `alpha` until convergence.

# Key Components

- **MODULE MMaximumEntropy:** [Requires manual description]
  - **SUBROUTINE w2maxent:** [Requires manual description] (The main driver routine for the Maximum Entropy calculation. It initializes the spectral function, kernel, and likelihood curvature. It then enters a loop, performing Monte Carlo steps to find the most probable spectral function for a given `alpha`, and then updates `alpha` based on Bayesian inference criteria until convergence. After convergence, it can perform smoothing steps.)
  - **SUBROUTINE initKernel:** [Requires manual description] (Initializes the kernel `K(w, tau/iwn)` that relates the spectral function to the input Green's function data. It handles different `kernelMode` options for various input data types like G(tau), G(iwn), and bosonic susceptibilities.)
  - **SUBROUTINE initLikelihoodCurvature:** [Requires manual description] (Calculates the curvature tensor of the log-likelihood function, which is used in the Bayesian update of `alpha`.)
  - **SUBROUTINE bayesianInverence:** [Requires manual description] (Performs the Bayesian inference step to check for convergence and update the `alpha` parameter based on the current spectral function and likelihood curvature.)
  - **SUBROUTINE montecarloSpectralFunction:** [Requires manual description] (Performs a simulated annealing Monte Carlo algorithm to find the spectral function that maximizes the posterior probability for a fixed `alpha`.)
  - **SUBROUTINE smoothSpectrum:** [Requires manual description] (Applies smoothing to the converged spectral function using different available methods.)
  - **SUBROUTINE chiMoments:** [Requires manual description] (Calculates moments of a susceptibility, like `chi(omega=0)` and `chi(tau=0)`, from the spectral function for bosonic kernels.)
  - **SUBROUTINE getGridUnit:** [Requires manual description] (Calculates integration weights for the spectral grid, supporting trapezoidal rule or uniform spacing.)
  - **SUBROUTINE normalizeToGrid:** [Requires manual description] (Normalizes a function (spectral function or model) such that its integral over the grid is 1, for certain kernel modes.)
  - **SUBROUTINE writeLog:** [Requires manual description] (A utility subroutine for writing log messages to a file and optionally to the standard output.)

# Important Variables/Constants

- **Module-level parameters:** `bayesianConvergence`, `bayesianUpdateAlpha`, `noiseFilter`, `variationUpdate`, `criticaleAcceptRate`, `annealingParamWarmup`, etc. These control various aspects of the Bayesian inference and Monte Carlo optimization procedures.
- **`kernelMode`:** An integer parameter passed to `w2maxent` that specifies the type of input data and the corresponding integral kernel to be used.
[Requires manual identification and description of important variables/constants/common blocks]

# Usage Examples

[Requires manual addition of usage examples if applicable]

# Dependencies and Interactions

- **USE MMersenneTwister:** Used for random number generation (`grnd`) within the Monte Carlo routine.
- LAPACK routines (`DGETRF`, `DGETRI`) are used internally by `bayesianInverence` for matrix inversion when calculating `bayesTrace`.
- This module is typically called by a higher-level script (like the `MaxEnt.py` mentioned in the `w2dyn/maxent/__init__.py` docstring) that prepares the input data (Green's functions, error covariance, model) and then invokes `w2maxent`.
[Requires manual description of further interactions]
