# Overview

This file src/ctqmc_fortran/Nfft_worm.F90 contains...
This Fortran module, `ft_worm`, provides a subroutine `ft_nd` for performing n-dimensional Fourier transforms. It is designed to work with data from QMC estimators, particularly for "worm" algorithm measurements. The module has conditional compilation (`#ifdef USE_NFFT` / `#else` / `#endif`) to switch between using the NFFT library for non-equispaced data and a naive direct Fourier summation for testing or when NFFT is not available.

# Key Components

- **MODULE ft_worm:** [Requires manual description]
  - **SUBROUTINE ft_nd:** [Requires manual description]
    - **NFFT version (if `USE_NFFT` is defined):**
      - Takes non-equispaced time-domain data `x` (tau values) and corresponding function values `f`.
      - Initializes an NFFT plan using `nfft_init_guru` (from `nfft_interface`).
      - Sets up the plan with pointers to the input data `x` and `f`, and the output array `f_hat`.
      - Calls `nfft_precompute_one_psi` if required by the plan flags.
      - Performs the adjoint NFFT (non-equispaced data to regular frequency grid) using `nfft_adjoint`.
      - Finalizes the NFFT plan.
    - **Naive version (if `USE_NFFT` is not defined):**
      - Takes time-domain data `x` and function values `f`.
      - Manually constructs a regular frequency grid `omega`.
      - Performs a direct summation: `f_hat(omega) = sum_j exp(i * omega_k * x_j) * f(x_j)`.
- **PROGRAM ft_test:** [Requires manual description] (A test program included if `FT_Test` is defined. It generates sample data and calls `ft_nd` to test the Fourier transform implementation, writing the results to files.)

# Important Variables/Constants

[Requires manual identification and description of important variables/constants/common blocks]

# Usage Examples

[Requires manual addition of usage examples if applicable]

# Dependencies and Interactions

- **USE MParameters:** Likely provides kind parameters for real and complex numbers.
- **USE iso_c_binding:** Used for C interoperability, especially in the NFFT version for defining C types and pointers.
- **USE nfft_static, nfft_interface:** (Conditional, if `USE_NFFT` is defined) These modules (from `Nfft_base.F90`) provide the Fortran type definition for `nfft_plan` and interfaces to the C NFFT library functions.
- Relies on an external NFFT library and potentially FFTW library if the NFFT version is compiled and used.
[Requires manual description of further interactions]
