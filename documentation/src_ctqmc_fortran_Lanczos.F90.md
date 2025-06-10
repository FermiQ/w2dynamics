# Overview

This file src/ctqmc_fortran/Lanczos.F90 contains...
This Fortran module, `MLanczos`, implements the Lanczos algorithm for operations within a quantum many-body system, likely related to the CT-QMC solver. The Lanczos algorithm is used here for:
- Finding eigenvalues and eigenvectors of a Hamiltonian (specifically the ground state energy and vector).
- Performing time evolution of a state vector.

The module includes subroutines for individual Lanczos steps, calculating the ground state energy (`LanczosE0`), the ground state vector (`LanczosV0`), transforming vectors back from Krylov space (`LanczosTransform`), and the main time evolution routine (`LanczosTimeEvolve`). It also contains helper subroutines for tridiagonal matrix operations (`TriEigen`, `MatInvert`).

# Key Components

- **MODULE MLanczos:** [Requires manual description]
  - **SUBROUTINE LanczosStep:** [Requires manual description] (Performs a single step of the Lanczos iteration, calculating the Lanczos coefficients `a` and `b`.)
  - **SUBROUTINE LanczosE0:** [Requires manual description] (Calculates the ground state energy `Egs` and related quantities by performing multiple Lanczos steps and diagonalizing the resulting tridiagonal matrix.)
  - **SUBROUTINE LanczosV0:** [Requires manual description] (Calculates the ground state eigenvector `Psi0` using the Lanczos vectors and eigenvectors of the tridiagonal matrix.)
  - **SUBROUTINE LanczosTransform:** [Requires manual description] (Transforms a vector from the Krylov basis (Lanczos vectors) back to the original state space.)
  - **SUBROUTINE LanczosTimeEvolve:** [Requires manual description] (Performs time evolution of an input state `Psi_t` to `Psi_tp` over a time `tau` using the Lanczos algorithm.)
  - **SUBROUTINE TriEigen:** [Requires manual description] (Calculates eigenvalues and eigenvectors of a symmetric tridiagonal matrix.)
  - **SUBROUTINE MatInvert:** [Requires manual description] (Calculates the inverse of a matrix, with specific optimizations for small dimensions and falling back to LAPACK routines for larger matrices.)
- **PROGRAM Prog_Lanczos:** [Requires manual description] (A test program included if `Lanczos_Test` is defined, used to test the Lanczos routines.)

# Important Variables/Constants

- **PMAX:** (Implicitly used, likely defined in `MParameters` or `MStates`) The maximum dimension of the Krylov space / Lanczos vectors.
- **EPSLANC:** (Implicitly used) A tolerance for convergence in the Lanczos algorithm.
[Requires manual identification and description of important variables/constants/common blocks]

# Usage Examples

[Requires manual addition of usage examples if applicable]

# Dependencies and Interactions

- **USE MStates:** Provides `TStates` type (for state information) and possibly `PMAX`.
- **USE MSparseMatrix:** Provides `SMatVecProdAdd` and `MatVecProd` for sparse matrix-vector products (Hamiltonian application).
- LAPACK routines (`dstev` or `stev`, `DGETRF` or `GETRF`, `DGETRI` or `GETRI`, `ZLACPY`, `ZGEEV` or `LA_GEEV`) are used for matrix operations (tridiagonal diagonalization, matrix inversion, general eigenvalue problems), with conditional compilation for different LAPACK interfaces (`LAPACK77_Interface` vs `LAPACK95_Interface`).
[Requires manual description of further interactions]
