# Overview

This file Random.F90 contains...
This Fortran module, `MRandom`, provides an interface to a C++ based pseudo-random number generator (PRNG), likely implemented in `random.cc`. It uses ISO C Binding to call C functions for creating, seeding, deleting, and using the PRNG. The module maintains a singleton instance of the PRNG.

# Key Components

- **MODULE MRandom:** [Requires manual description]
  - **INTERFACE (for C functions):** [Requires manual description]
    - **FUNCTION new_random (bind(C)):** [Requires manual description] (Likely calls a C function to create a new PRNG instance and return a pointer to it.)
    - **SUBROUTINE delete_random (bind(C)):** [Requires manual description] (Likely calls a C function to delete a PRNG instance.)
    - **SUBROUTINE seed_random (bind(C)):** [Requires manual description] (Likely calls a C function to seed the PRNG.)
    - **FUNCTION get_random (bind(C)):** [Requires manual description] (Likely calls a C function to get a random double precision number from the PRNG.)
    - **FUNCTION get_randint (bind(C)):** [Requires manual description] (Likely calls a C function to get a random integer within a specified range from the PRNG.)
  - **SUBROUTINE sgrnd:** [Requires manual description] (Initializes or re-initializes the singleton PRNG. If an instance exists, it's deleted, then a new one is created and seeded.)
  - **FUNCTION grnd:** [Requires manual description] (Returns a random double precision number in [0,1) by calling the C `get_random` function via the interface.)
  - **FUNCTION randint:** [Requires manual description] (Returns a random integer in the specified range `[min, max]` by calling the C `get_randint` function.)

# Important Variables/Constants

- **VARIABLE singleton (type(c_ptr), save):** [Requires manual description] (A module-level variable that holds a C pointer to the single instance of the PRNG. Initialized to `C_NULL_PTR`.)
[Requires manual identification and description of important variables/constants/common blocks]

# Usage Examples

[Requires manual addition of usage examples if applicable]
```fortran
USE MRandom

REAL(KIND(0.D0)) :: r_val
INTEGER :: i_val

CALL sgrnd(12345) ! Seed the generator

r_val = grnd()
WRITE(*,*) "Random double:", r_val

i_val = randint(1, 100)
WRITE(*,*) "Random integer between 1 and 100:", i_val
```

# Dependencies and Interactions

- **USE ISO_C_BINDING:** Used extensively for defining C types (`c_ptr`, `c_int`, `c_double`) and for the `bind(C)` attribute in the interface block, enabling interoperability with C/C++ code.
- This module is a Fortran wrapper around a C/C++ PRNG. The actual random number generation logic resides in the C/C++ code (e.g., `random.cc`).
[Requires manual description of further interactions]
