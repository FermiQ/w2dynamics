# Overview

This file src/ctqmc_fortran/Parameters.F90 contains...
This Fortran module, `MParameters`, is responsible for managing and providing access to simulation parameters. It defines kind parameters for real and complex numbers (`KINDR`, `KINDC`), various constants (like `PMAX`, `stdin`, `stdout`, `stderr`, error codes, string lengths), and parameters related to QMC worm algorithm sectors.

The core functionality revolves around a linked list of `TParameter` types, where each node stores a parameter ID (string) and its value (string). The module provides routines to:
- Read parameters from an input file (`read_ParameterFile`) or a string (`read_ParameterString`).
- Retrieve parameter values as integers (`get_Integer_Parameter`, `get_LongInteger_Parameter`), reals (`get_Real_Parameter`), lists of reals/integers (`get_Real_List`, `get_Integer_List`), or strings (`get_String_Parameter`).
- Set/update a parameter value (`set_Parameter`).
- Deallocate the parameter list (`dest_Parameters`).

# Key Components

- **MODULE MParameters:** [Requires manual description]
  - **TYPE TParameter (private):** [Requires manual description] (Derived type to store a parameter ID, its string value, and a pointer to the next parameter.)
  - **FUNCTION eq:** [Requires manual description] (Elemental function to compare two real numbers for equality within a tolerance.)
  - **SUBROUTINE set_Parameter:** [Requires manual description] (Sets or updates the value of an existing parameter.)
  - **FUNCTION get_Integer_Parameter:** [Requires manual description] (Retrieves a parameter value as an integer.)
  - **FUNCTION get_LongInteger_Parameter:** [Requires manual description] (Retrieves a parameter value as a 64-bit integer.)
  - **FUNCTION get_Real_Parameter:** [Requires manual description] (Retrieves a parameter value as a real number.)
  - **SUBROUTINE get_Real_List:** [Requires manual description] (Retrieves a list of real parameter values.)
  - **SUBROUTINE get_Integer_List:** [Requires manual description] (Retrieves a list of integer parameter values.)
  - **FUNCTION get_String_Parameter:** [Requires manual description] (Retrieves a parameter value as a string.)
  - **SUBROUTINE push_Parameter:** [Requires manual description] (Adds a new parameter to the linked list.)
  - **SUBROUTINE read_ParameterFile:** [Requires manual description] (Reads parameters from a file, parsing lines of "ID = Value # comment" format.)
  - **SUBROUTINE read_ParameterString:** [Requires manual description] (Reads parameters from a single string containing multiple newline-separated parameter definitions.)
  - **SUBROUTINE dest_Parameters:** [Requires manual description] (Deallocates the linked list of parameters.)
- **PROGRAM Prog_Parameters:** [Requires manual description] (A test program included if `Parameters_Test` is defined.)

# Important Variables/Constants

- **KINDR, KINDC:** Integer parameters defining the kind for real and complex numbers.
- **PMAX:** Integer parameter, likely a maximum dimension for arrays (e.g., Lanczos vectors).
- **EPSLANC, EPSDEG:** Real parameters for numerical tolerances.
- **SectorZ, SectorG, ..., SectorQUDdag:** Integer parameters defining QMC worm sector indices.
- **NOperWorm:** Integer array defining the number of operators for each worm sector.
- **first, last (private):** Pointers to the head and tail of the linked list of parameters.
[Requires manual identification and description of important variables/constants/common blocks]

# Usage Examples

[Requires manual addition of usage examples if applicable]

# Dependencies and Interactions

- **USE iso_c_binding:** Used for `c_int64_t` and `c_long_double`.
- This module is fundamental for the CTQMC code, as it provides the mechanism for reading and accessing all runtime parameters.
[Requires manual description of further interactions]
