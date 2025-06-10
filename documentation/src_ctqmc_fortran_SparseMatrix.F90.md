# Overview

This file src/ctqmc_fortran/SparseMatrix.F90 contains...
This Fortran module, `MSparseMatrix`, implements a sparse matrix representation using the Compressed Sparse Row (CSR) format and provides routines for sparse matrix-vector multiplication.

The CSR format is stored using three arrays:
- `dat`: Contains the non-zero values of the matrix.
- `indices`: Contains the column indices corresponding to the values in `dat`.
- `ptr`: An array where `ptr(i)` points to the start of row `i` in `dat` and `indices`. `ptr(dim1+1)` stores one beyond the total number of non-zero elements.

# Key Components

- **MODULE MSparseMatrix:** [Requires manual description]
  - **TYPE TSparseMatrix:** [Requires manual description] (Derived type to store a sparse matrix in CSR format.)
    - `dim1`: Integer, the first dimension (number of rows) of the matrix.
    - `ptr`: Allocatable integer array for row pointers.
    - `indices`: Allocatable integer array for column indices.
    - `dat`: Allocatable `real(KINDR)` array for non-zero data values.
  - **SUBROUTINE init_SparseMatrix:** [Requires manual description] (Initializes a `TSparseMatrix` from a dense `real(KINDR)` matrix. It counts non-zero elements and populates the `dat`, `indices`, and `ptr` arrays.)
  - **FUNCTION MatVecProd:** [Requires manual description] (Performs matrix-vector product `y = A*x` where `A` is a `TSparseMatrix` and `x` is a dense vector. Returns the dense vector `y`.)
  - **SUBROUTINE SMatVecProd:** [Requires manual description] (Similar to `MatVecProd` but returns the result `y` as an output argument.)
  - **SUBROUTINE SMatVecProdAdd:** [Requires manual description] (Performs `y = y + A*x`.)
  - **SUBROUTINE print_SparseMatrix:** [Requires manual description] (Prints the sparse matrix content in a "Row/Col/Data" format.)
  - **SUBROUTINE dest_SparseMatrix:** [Requires manual description] (Deallocates the arrays within a `TSparseMatrix` object.)
- **PROGRAM Prog_SparseMatrix:** [Requires manual description] (A test program included if `SparseMatrix_Test` is defined. It creates a sparse matrix from a sample dense matrix, prints it, performs a matrix-vector product, compares with `MATMUL` on the dense matrix, and then deallocates the sparse matrix.)

# Important Variables/Constants

[Requires manual identification and description of important variables/constants/common blocks]

# Usage Examples

[Requires manual addition of usage examples if applicable]

# Dependencies and Interactions

- **USE MParameters:** Used for the `KINDR` kind parameter and the `eq` function for comparing real numbers with a tolerance (to determine non-zero elements).
[Requires manual description of further interactions]
