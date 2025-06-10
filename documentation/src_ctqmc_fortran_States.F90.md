# Overview

This file src/ctqmc_fortran/States.F90 contains...
This Fortran module, `MStates`, defines data structures and routines for managing the quantum states of a system, particularly for use in a CT-QMC simulation. It handles the Fock space, grouping of states into "superstates" (or blocks) based on good quantum numbers (like total particle number `Nt`, total spin projection `Szt`), and provides information about connections between these superstates via creation/annihilation operators.

# Key Components

- **MODULE MStates:** [Requires manual description]
  - **TYPE TStates:** [Requires manual description] (Main derived type to hold information about the system's states.)
    - `NBands`: Number of orbitals.
    - `NStates`: Total number of states in the Fock space.
    - `NSStates`: Number of superstates (blocks).
    - `NStatesMax`: Maximum number of states in any single superstate.
    - `StatesSStates`: Pointer to an array mapping integer representation of a state to its superstate and its own index.
    - `SubStates`: Pointer to an array of `TSubStates`.
  - **TYPE TStates_pointer:** [Requires manual description] (A type to hold a pointer to a `TStates` object.)
  - **TYPE TPsis_EB:** [Requires manual description] (Holds an operator (e.g., creation/annihilation) in the eigenbasis.)
  - **TYPE TSubStates:** [Requires manual description] (Represents a superstate/block.)
    - `NStates`: Number of states in this superstate.
    - `Offset`: Offset for this superstate's eigenvalues/vectors in larger arrays.
    - `Connect`: Pointer to an array indicating which superstate is reached by applying an operator.
    - `States`: Pointer to an array of integer representations of states in this superstate.
    - `Psis`: Pointer to an array of `TSparseMatrix` for creation/annihilation operators in occupation basis.
    - `Psis_EB`: Pointer to an array of `TPsis_EB` for creation/annihilation operators in eigenbasis.
    - `Hamiltonian`: Pointer to a `TSparseMatrix` for the Hamiltonian block.
    - `EVal`: Pointer to an array of eigenvalues for this block.
    - `EVec`: Pointer to an array of eigenvectors for this block.
    - `S2`: Pointer to the S^2 operator matrix for this block.
  - **SUBROUTINE init_States:** [Requires manual description] (Initializes the `TStates` type, setting up the `StatesSStates` mapping. Can read initial occupations from `occup.dat`.)
  - **SUBROUTINE init_substates:** [Requires manual description] (Initializes the `SubStates` array within `TStates` based on a pre-computed `states2substates` mapping.)
  - **SUBROUTINE qns2substates:** [Requires manual description] (Determines superstates by grouping states that have the same specified good quantum numbers read from parameters.)
  - **FUNCTION get_Nt:** [Requires manual description] (Calculates the total number of electrons for a given state.)
  - **FUNCTION get_Szt:** [Requires manual description] (Calculates the total Sz projection for a given state.)
  - **FUNCTION get_Qzt, get_Azt, get_Lzt, get_Jzt:** [Requires manual description] (Calculate other potential quantum numbers.)
  - **FUNCTION get_eg_up, get_eg_do, get_t2g_up, get_t2g_do:** [Requires manual description] (Calculate occupations for specific orbital groups, likely eg and t2g for d-orbitals.)
  - **FUNCTION get_occ:** [Requires manual description] (Pure function to get occupation of a specific orbital and spin.)
  - **FUNCTION get_OccStr:** [Requires manual description] (Returns a string representation of a state's occupation, e.g., "|101|010>".)
  - **SUBROUTINE print_States:** [Requires manual description] (Prints all states with their Nt and Szt.)
  - **SUBROUTINE print_JanStates:** [Requires manual description] (Prints states with more detailed quantum number breakdown.)
  - **SUBROUTINE print_SubStates:** [Requires manual description] (Prints information about each superstate and the states it contains.)
  - **SUBROUTINE print_densitymatrix_basis:** [Requires manual description] (Prints basis information relevant to the density matrix to a file.)
  - **SUBROUTINE dest_States:** [Requires manual description] (Deallocates all allocatable components of a `TStates` object.)
- **PROGRAM States_Prog:** [Requires manual description] (A test program included if `States_Test` is defined.)

# Important Variables/Constants

[Requires manual identification and description of important variables/constants/common blocks]

# Usage Examples

[Requires manual addition of usage examples if applicable]

# Dependencies and Interactions

- **USE MParameters:** For kind parameters, string lengths, and parameter access functions (e.g., `get_String_Parameter`, `get_Integer_Parameter`).
- **USE MSparseMatrix:** For the `TSparseMatrix` type used within `TSubStates`.
- **USE MAusgabe:** For formatted printing in the test program.
- This module is central to defining the Hilbert space and its symmetries for the QMC calculation. It is heavily used by `MOperator` for constructing operator matrices and by `MTrace` and `MCTQMC` for performing simulations.
[Requires manual description of further interactions]
