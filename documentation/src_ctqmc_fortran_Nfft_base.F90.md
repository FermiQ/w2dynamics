# Overview

This file src/ctqmc_fortran/Nfft_base.F90 contains...
This Fortran source file defines two modules related to the NFFT (Non-equispaced Fast Fourier Transform) library, primarily for interfacing with its C implementation.

- **MODULE nfft_static:** This module defines a Fortran derived type `nfft_plan` that mirrors the `nfft_plan` structure in the C NFFT library. This allows Fortran code to create and manage NFFT plan objects. It also defines various integer parameters that correspond to NFFT flags (e.g., `PRE_PSI`, `MALLOC_X`, `FFTW_ESTIMATE`), likely used to control the behavior of the NFFT routines.

- **MODULE nfft_interface:** This module declares Fortran interfaces to several C functions from the NFFT library. These interfaces specify the Fortran equivalent of the C function signatures, enabling Fortran code to call these C NFFT routines for initializing plans (`nfft_init_1d`, `nfft_init_2d`, `nfft_init_3d`, `nfft_init_guru`), precomputing parts of the transform (`nfft_precompute_one_psi`), performing the adjoint transform (`nfft_adjoint`), checking the plan (`nfft_check`), and finalizing/destroying the plan (`nfft_finalize`).

# Key Components

- **MODULE nfft_static:** [Requires manual description]
  - **TYPE nfft_plan:** [Requires manual description] (Fortran equivalent of the C NFFT plan structure.)
  - **PARAMETER PRE_PHI_HUT, FG_PSI, etc.:** [Requires manual description] (Integer parameters representing NFFT flags.)
- **MODULE nfft_interface:** [Requires manual description]
  - **INTERFACE nfft_init_1d, nfft_init_2d, nfft_init_3d, nfft_init_guru:** [Requires manual description] (Interfaces to NFFT plan initialization functions.)
  - **INTERFACE nfft_precompute_one_psi:** [Requires manual description] (Interface to NFFT precomputation function.)
  - **INTERFACE nfft_adjoint:** [Requires manual description] (Interface to NFFT adjoint transform function.)
  - **INTERFACE nfft_check:** [Requires manual description] (Interface to NFFT plan checking function.)
  - **INTERFACE nfft_finalize:** [Requires manual description] (Interface to NFFT plan finalization function.)

# Important Variables/Constants

- The various integer parameters within `nfft_static` (e.g., `PRE_ONE_PSI`, `FFTW_INIT`) are crucial for configuring the NFFT library calls.
[Requires manual identification and description of important variables/constants/common blocks]

# Usage Examples

[Requires manual addition of usage examples if applicable]

# Dependencies and Interactions

- **USE iso_c_binding:** Used extensively in both modules for C interoperability, defining C types (`c_int`, `c_ptr`, `c_double`, `c_funptr`, `c_intptr_t`) and the `bind(C)` attribute.
- This file provides the Fortran-side definitions and interfaces to an external C library (NFFT). Other Fortran modules that use NFFT would `USE` these modules.
[Requires manual description of further interactions]
