# Overview

This file src/ctqmc_fortran/Accumulators.F90 contains...
This Fortran module defines different types of accumulators for collecting and processing data, likely from Monte Carlo simulations. It provides a base accumulator type and specialized versions for calculating means and autocorrelation functions. The accumulators are designed to handle data efficiently, with considerations for time and memory costs.

# Key Components

- **MODULE accumulators:** [Requires manual description]
  - **TYPE accumulator:** [Requires manual description] (Base type for accumulators)
    - **PROCEDURE add => accumulator_add:** [Requires manual description]
    - **PROCEDURE reset => accumulator_reset:** [Requires manual description]
    - **PROCEDURE delete => accumulator_delete:** [Requires manual description]
    - **PROCEDURE num_comp => accumulator_num_comp:** [Requires manual description]
    - **PROCEDURE num_blocks => accumulator_na:** [Requires manual description]
    - **PROCEDURE has_mean => accumulator_no:** [Requires manual description]
    - **PROCEDURE has_blocks => accumulator_no:** [Requires manual description]
    - **PROCEDURE get_mean => accumulator_handle1d:** [Requires manual description]
    - **PROCEDURE get_blocks => accumulator_handle2d:** [Requires manual description]
  - **TYPE meanacc (extends accumulator):** [Requires manual description] (Accumulator for mean values)
    - **PROCEDURE add => meanacc_add:** [Requires manual description]
    - **PROCEDURE reset => meanacc_reset:** [Requires manual description]
    - **PROCEDURE delete => meanacc_delete:** [Requires manual description]
    - **PROCEDURE has_mean => meanacc_has_mean:** [Requires manual description]
    - **PROCEDURE get_mean => meanacc_mean:** [Requires manual description]
  - **TYPE varatom:** [Requires manual description] (Helper type for `autocorracc`)
  - **TYPE autocorracc (extends accumulator):** [Requires manual description] (Accumulator for means, variances, and autocorrelation analysis)
    - **PROCEDURE add => autocorracc_add:** [Requires manual description]
    - **PROCEDURE reset => autocorracc_reset:** [Requires manual description]
    - **PROCEDURE delete => autocorracc_delete:** [Requires manual description]
    - **PROCEDURE has_mean => autocorracc_has_mean:** [Requires manual description]
    - **PROCEDURE has_blocks => autocorracc_has_blocks:** [Requires manual description]
    - **PROCEDURE num_blocks => autocorracc_num_blocks:** [Requires manual description]
    - **PROCEDURE get_mean => autocorracc_mean:** [Requires manual description]
    - **PROCEDURE get_blocks => autocorracc_blocks:** [Requires manual description]
  - **FUNCTION ilog2:** [Requires manual description]
  - **FUNCTION accumulator_create:** [Requires manual description]
  - **SUBROUTINE accumulator_reset:** [Requires manual description]
  - **SUBROUTINE accumulator_delete:** [Requires manual description]
  - **SUBROUTINE accumulator_add:** [Requires manual description]
  - **FUNCTION accumulator_no:** [Requires manual description]
  - **FUNCTION accumulator_num_comp:** [Requires manual description]
  - **FUNCTION accumulator_na:** [Requires manual description]
  - **SUBROUTINE accumulator_handle1d:** [Requires manual description]
  - **SUBROUTINE accumulator_handle2d:** [Requires manual description]
  - **FUNCTION meanacc_create:** [Requires manual description]
  - **SUBROUTINE meanacc_reset:** [Requires manual description]
  - **FUNCTION meanacc_has_mean:** [Requires manual description]
  - **SUBROUTINE meanacc_delete:** [Requires manual description]
  - **SUBROUTINE meanacc_add:** [Requires manual description]
  - **SUBROUTINE meanacc_mean:** [Requires manual description]
  - **FUNCTION autocorracc_create:** [Requires manual description]
  - **SUBROUTINE autocorracc_delete:** [Requires manual description]
  - **SUBROUTINE autocorracc_reset:** [Requires manual description]
  - **FUNCTION autocorracc_has_mean:** [Requires manual description]
  - **FUNCTION autocorracc_has_blocks:** [Requires manual description]
  - **FUNCTION autocorracc_num_blocks:** [Requires manual description]
  - **SUBROUTINE autocorracc_resize:** [Requires manual description]
  - **SUBROUTINE autocorracc_add:** [Requires manual description]
  - **SUBROUTINE autocorracc_mean:** [Requires manual description]
  - **SUBROUTINE autocorracc_blocks:** [Requires manual description]
- **PROGRAM test_program:** [Requires manual description] (A test program included if `ACC_TEST_PROGRAM` is defined)

# Important Variables/Constants

- **PARAMETER nan:** Defines a Not-a-Number (NaN) value, with a preprocessor guard for different gfortran versions.
[Requires manual identification and description of important variables/constants/common blocks]

# Usage Examples

[Requires manual addition of usage examples if applicable]

# Dependencies and Interactions

- **USE iso_c_binding:** Used for `c_int64_t` and `c_double` for C interoperability.
[Requires manual description of further interactions]
