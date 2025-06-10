# Overview

This file src/ctqmc_fortran/Nfft_z.F90 contains...
This Fortran source file defines modules related to Fourier transforms, specifically providing a fallback mechanism if the NFFT library is not used, and a common module for Fourier transform parameters.

- **MODULE nfft_fallback:** This module provides stub implementations for some NFFT interface functions if the `USE_NFFT` preprocessor macro is not defined. This allows the code to compile and run with a basic, likely slower, direct Fourier summation as a fallback. It uses C's `malloc` and `free` for memory management within its stubbed `nfft_init_1d` and `nfft_finalize`. The `nfft_adjoint` stub performs a direct summation for the adjoint Fourier transform.

- **MODULE ft_common:** This module stores common parameters used in Fourier transforms, such as the number of frequencies (`nfreq`, `n2freq`) and the inverse temperature (`beta`). It provides an initialization subroutine `ft_common_init` to set these parameters.

- **MODULE ft_fast (if `USE_NFFT` is defined):** This module is intended to provide fast Fourier transform routines using the NFFT library. It includes `ft_init` and `ft_cleanup` (currently empty stubs) and two main functions:
    - `get_giw`: Computes the Green's function in Matsubara frequencies from hybridization matrix data using NFFT. It handles the transformation from tau differences to Matsubara frequencies.
    - `get_giw2`: A variation of `get_giw`.
    - `get_g2iw`: Computes the two-time Green's function G(iw, iw') using a 2D NFFT.

- **MODULE ft_naive (if `USE_NFFT` is NOT defined):** This module provides naive (direct summation) implementations for `get_giw` and `get_g2iw` as a fallback when NFFT is not used.

- **PROGRAM test_nfft (if `nfft_Test` is defined):** A test program for the NFFT interface.

# Key Components

- **MODULE nfft_fallback:** [Requires manual description]
  - **SUBROUTINE warn_fallback:** [Requires manual description]
  - **SUBROUTINE nfft_init_1d, nfft_init_2d, nfft_finalize, nfft_precompute_one_psi, nfft_adjoint:** [Requires manual description] (Stub implementations for NFFT interface functions.)
- **MODULE ft_common:** [Requires manual description]
  - **SUBROUTINE ft_common_init:** [Requires manual description] (Initializes common FT parameters.)
- **MODULE ft_fast (conditional):** [Requires manual description]
  - **SUBROUTINE ft_init:** [Requires manual description]
  - **SUBROUTINE ft_cleanup:** [Requires manual description]
  - **FUNCTION get_giw:** [Requires manual description] (Computes G(iw) using NFFT.)
  - **FUNCTION get_giw2:** [Requires manual description] (Variant of get_giw.)
  - **FUNCTION get_g2iw:** [Requires manual description] (Computes G(iw, iw') using 2D NFFT.)
- **MODULE ft_naive (conditional):** [Requires manual description]
  - **SUBROUTINE ft_init:** [Requires manual description]
  - **SUBROUTINE ft_cleanup:** [Requires manual description]
  - **FUNCTION get_giw:** [Requires manual description] (Computes G(iw) using direct summation.)
  - **FUNCTION get_g2iw:** [Requires manual description] (Computes G(iw, iw') using direct summation.)
- **PROGRAM test_nfft:** [Requires manual description] (A test program for NFFT functionality.)

# Important Variables/Constants

- Variables within `ft_common`: `nfreq`, `n2freq`, `beta`.
[Requires manual identification and description of important variables/constants/common blocks]

# Usage Examples

[Requires manual addition of usage examples if applicable]

# Dependencies and Interactions

- **USE MParameters:** For `KINDR`.
- **USE iso_c_binding:** For C interoperability.
- **USE LegendrePoly:** For `PI`.
- **USE nfft_static, nfft_interface:** (Conditional, if `USE_NFFT` is defined) For NFFT types and C function interfaces.
- Relies on an external NFFT library and FFTW if `USE_NFFT` is defined.
- Interacts with other modules that require Fourier transforms of QMC data.
[Requires manual description of further interactions]
