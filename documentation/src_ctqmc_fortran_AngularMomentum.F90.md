# Overview

This file src/ctqmc_fortran/AngularMomentum.F90 contains...
This Fortran module, `MAngularMomentum`, provides functions for calculating various quantities related to angular momentum theory. These include factorials (for integers and half-integers), Wigner 3-jm symbols, Gaunt coefficients, and Clebsch-Gordan coefficients. It also contains a subroutine to calculate Legendre polynomials. The module mentions the possibility of caching 3-jm symbols for performance, though it's not currently implemented. It also defines Pauli spin matrices and spin creation/annihilation operators as parameters.

# Key Components

- **MODULE MAngularMomentum:** [Requires manual description]
  - **TYPE T3jm:** [Requires manual description] (A type to potentially store 3jm symbols and their parameters, currently not fully utilized for caching.)
  - **FUNCTION get_fact:** [Requires manual description] (Calculates and caches factorials.)
  - **FUNCTION get_3jm:** [Requires manual description] (Calculates Wigner 3-jm symbols.)
  - **FUNCTION get_gaunt:** [Requires manual description] (Calculates Gaunt coefficients using 3-jm symbols.)
  - **FUNCTION get_clebschgordan:** [Requires manual description] (Calculates Clebsch-Gordan coefficients using 3-jm symbols.)
  - **SUBROUTINE legendre_poly:** [Requires manual description] (Calculates Legendre polynomials recursively.)
- **PROGRAM AngularMomentum_Prog:** [Requires manual description] (A test program included if `AngularMomentum_Test` is defined, used to test the functions in the module.)

# Important Variables/Constants

- **PARAMETER PauliSM:** 3D array representing the Pauli spin matrices.
- **PARAMETER Spm:** 3D array representing spin creation/annihilation operators.
- **VARIABLE fact:** A real array used to cache calculated factorial values for faster lookup.
[Requires manual identification and description of important variables/constants/common blocks]

# Usage Examples

[Requires manual addition of usage examples if applicable]

# Dependencies and Interactions

- **USE MParameters:** This module is used, likely providing definitions for `KINDR` and `KINDC` (kind parameters for real and complex numbers).
[Requires manual description of further interactions]
