# Overview

This file src/ctqmc_fortran/MatrixUpdate.F90 contains...
This Fortran module, `MMatrixUpdate`, provides routines for calculating determinants and inverses of matrices, with a focus on efficiently updating these quantities when rows/columns are added or removed. This is particularly useful in QMC methods where matrices (like hybridization matrices) change incrementally. It defines a custom type `TLogDet` to store the logarithm of the absolute determinant and its sign, which helps in handling very large or small determinant values.

The module includes:
- Functions for LU decomposition-based full matrix determinant (`get_LogDetFull`) and inverse (`get_MatLogDetFull`).
- Functions for fast updates of determinants and inverses using the Sherman-Morrison formula or related methods for rank-1 updates (adding/removing a row and column): `get_DetRatAdd`, `get_MatAdd`, `get_DetRatRem`, `get_MatRem`.
- Commented-out sections suggest that versions using Singular Value Decomposition (SVD) via LAPACK's `DBDSQR` or `DBDSDC` were considered or partially implemented but are not currently active.

# Key Components

- **MODULE MMatrixUpdate:** [Requires manual description]
  - **TYPE TLogDet:** [Requires manual description] (Stores log(abs(det)) and sign(det).)
  - **INTERFACE OPERATOR(*):** [Requires manual description] (Overloads `*` for `TLogDet`.)
    - **MODULE PROCEDURE multiplyLogDet:** [Requires manual description]
  - **INTERFACE OPERATOR(/):** [Requires manual description] (Overloads `/` for `TLogDet`.)
    - **MODULE PROCEDURE divideLogDet:** [Requires manual description]
  - **FUNCTION multiplyLogDet:** [Requires manual description] (Multiplies two `TLogDet` types.)
  - **FUNCTION divideLogDet:** [Requires manual description] (Divides two `TLogDet` types.)
  - **FUNCTION detval:** [Requires manual description] (Converts `TLogDet` back to a standard real determinant value.)
  - **SUBROUTINE get_MatLogDetFull:** [Requires manual description] (Calculates determinant (as `TLogDet`) and inverse of a matrix using LU decomposition via LAPACK.)
  - **SUBROUTINE get_LogDetFull:** [Requires manual description] (Calculates determinant (as `TLogDet`) of a matrix using LU decomposition via LAPACK.)
  - **FUNCTION get_DetRatAdd:** [Requires manual description] (Calculates the ratio of determinants when adding a row/column.)
  - **FUNCTION get_MatAdd:** [Requires manual description] (Calculates the new inverse matrix after adding a row/column using Sherman-Morrison type update.)
  - **FUNCTION get_DetRatRem:** [Requires manual description] (Calculates the ratio of determinants when removing a row/column.)
  - **FUNCTION get_MatRem:** [Requires manual description] (Calculates the new inverse matrix after removing a row/column.)
- **PROGRAM Prog_MatrixUpdate:** [Requires manual description] (A test program included if `MatrixUpdate_Test` is defined, to test the matrix update routines.)

# Important Variables/Constants

[Requires manual identification and description of important variables/constants/common blocks]

# Usage Examples

[Requires manual addition of usage examples if applicable]

# Dependencies and Interactions

- **USE MParameters:** Likely provides `KINDR` (kind parameter for real numbers).
- LAPACK routines (`DGETRF` or `GETRF`, `DGETRI` or `GETRI`) are used for LU decomposition and matrix inversion. Conditional compilation (`LAPACK77_Interface` vs `LAPACK95_Interface`) suggests support for different LAPACK API versions.
[Requires manual description of further interactions]
