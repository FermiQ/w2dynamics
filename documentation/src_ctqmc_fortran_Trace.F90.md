# Overview

This file src/ctqmc_fortran/Trace.F90 contains...
This Fortran module, `MTrace`, is a crucial part of the CT-QMC algorithm, responsible for managing the sequence of operators in the Monte Carlo trace and calculating the weight (trace value) of the current configuration. Operators are stored in a time-ordered doubly-linked list. The module also handles flavour-specific linked lists for efficient updates.

Key functionalities include:
- Defining operator types (`TOper`) and structures for managing the trace (`TTrace`).
- Calculating the trace value, often involving Lanczos time evolution for segments of the trace or full trace evaluation in the eigenbasis (`get_Trace_EB`, `get_Trace_EB_fullmatrix`, `get_Trace_EB_onlyscalars`).
- Managing the hybridization matrix and its determinant/inverse, including fast updates when operators are added or removed (`get_InvFullHybr`, `get_LogDetRatPairAdd`, `get_LogDetRatPairRem`, etc.).
- Implementing QMC update moves:
    - Adding/removing pairs of hybridization operators (`StepAdd_mine`, `StepRem_mine` for segment picture; `StepAdd`, `StepRem`, `StepAdd4`, `StepRem4` for matrix-vector picture).
    - Global moves like spin flips and flavour exchanges (`StepGlob_mine`, `gen_GlobalUpdate_new`, `gen_SpinFlipUpdate`, `gen_SymUpdate`, `gen_CAFlip`).
    - Shifting operator times (`StepShiftTau_proper`, `StepChangeOuter`).
    - Worm algorithm moves for adding/removing worm operators or mixed worm/hybridization operators (`StepWormAdd`, `StepWormRem`, `StepWormHybAdd`, `StepWormHybRem`, `StepWormReplace`).
- Calculating proposal probabilities for worm moves (`get_Proposal`).
- Handling the sliding window for efficient updates (`init_window`, `shift_window`, `set_window`, `ensure_valid_NPairs`).
- Debugging and helper routines like printing the trace (`print_Trace`, `print_Trace_screen`).

# Key Components

- **MODULE MTrace:** [Requires manual description]
  - **TYPE TLogDet, TLogTr:** [Requires manual description] (Types for log-determinant and log-trace.)
  - **TYPE TOper:** [Requires manual description] (Represents an operator in the trace with time, flavour, and cached state vectors.)
  - **TYPE TSubArray, TSubMatrix, TOperPointer, TTrace_pointer, alloc_vector:** [Requires manual description] (Helper types.)
  - **TYPE TTrace:** [Requires manual description] (Main type holding the entire trace configuration, operator lists, hybridization matrices, etc.)
  - **FUNCTION multiplyLogDet, divideLogDet, detval, multiplyLogTr, divideLogTr, addLogTr, trval, wrat, flaveq:** [Requires manual description] (Elemental functions for `TLogDet` and `TLogTr` arithmetic and comparisons.)
  - **SUBROUTINE get_MatLogDetFull, get_LogDetFull, get_DetRatAdd, get_MatAdd, get_DetRatRem, get_MatRem, get_LogDetRatPairAdd_full, get_LogDetRatPairRem_full, add_ftau_offset:** [Requires manual description] (Matrix update routines, some likely moved from `MMatrixUpdate` or are specialized versions.)
  - **SUBROUTINE init_Trace, dest_Trace:** [Requires manual description] (Initialize and destroy the trace object.)
  - **SUBROUTINE minv_matching_taus:** [Requires manual description] (Matches taus for MInv.)
  - **FUNCTION get_HybrF, get_HybrF_full, get_lin_screening_function:** [Requires manual description] (Interpolate hybridization/screening functions.)
  - **SUBROUTINE rand_perm, gen_GlobalUpdate_new, gen_SpinFlipUpdate, gen_SymUpdate, gen_CAFlip, gen_InverseGlobalUpdate:** [Requires manual description] (Generate various global update proposals.)
  - **SUBROUTINE get_current_ssts, check_sst_sequence, perform_spinflip_check_qn, perform_global_check_qn, check_qn_all_ssts, save_outer_sst, restore_outer_sst:** [Requires manual description] (Quantum number and superstate checking for global moves.)
  - **FUNCTION WeightedOuterStateChoice:** [Requires manual description] (Chooses a new outer state based on weights.)
  - **SUBROUTINE init_window, shift_window, set_window, ensure_valid_NPairs, ensure_valid_NPairs_diag, ensure_valid_NPairs_offdiag, update_NPairs, update_NPairs_diag, update_NPairs_offdiag, ensure_valid_PreWinFCount, update_PreWinFCount:** [Requires manual description] (Sliding window management.)
  - **FUNCTION is_rempair, is_rempair_diag, is_rempair_offdiag:** [Requires manual description] (Check if an operator pair is removable.)
  - **FUNCTION get_Trace_EB, get_Trace_EB_onlyscalars, get_Trace_EB_fullmatrix, update_trace_EB, update_b2_states_eb:** [Requires manual description] (Core trace calculation routines.)
  - **SUBROUTINE meas_ntau_n0:** [Requires manual description] (Measures <n(tau)n(0)> correlation.)
  - **SUBROUTINE dump_mc_config_into_arrays, set_mc_config_from_arrays:** [Requires manual description] (Save/load MC configuration.)
  - **SUBROUTINE fresh_oper, duplicate_oper, recycle_oper:** [Requires manual description] (Operator memory management.)
  - **SUBROUTINE print_Trace, print_Trace_screen, print_Trace_flavour:** [Requires manual description] (Debugging output.)
  - **SUBROUTINE time_evolve_in_eigenbasis:** [Requires manual description]
  - **FUNCTION check_qn_add_eachflavour, get_sign_seg, check_equal_times, update_noscaoper, get_trace_seg_onestate_add, get_trace_seg_onestate_rem, get_trace_seg_flavourexchange, get_trace_seg_onestate, get_initial_amplum, treat_mu_part_onestate, treat_int_part_onestate:** [Requires manual description] (Segment algorithm specific routines.)
  - **SUBROUTINE StepAdd_mine, StepRem_mine, MeasOcc_seg, MeasSusz_seg, StepGlob_mine:** [Requires manual description] (Segment algorithm QMC moves.)
  - **SUBROUTINE propose_insert, my_insert_Oper, my_remove_Oper:** [Requires manual description] (Segment algorithm operator insertion/removal helpers.)
  - **FUNCTION propose_insert_seg, propose_remove_seg:** [Requires manual description] (Segment algorithm proposal generation.)
  - **SUBROUTINE get_fpos_insert:** [Requires manual description]
  - **FUNCTION get_Sign, recalc_sign, get_permaltca, get_BlockSign, get_WormSign:** [Requires manual description] (Calculate various sign contributions to the configuration weight.)
  - **SUBROUTINE pair_OperAdd, unrestricted_pair_OperAdd, flavor_OperAdd, density_OperAdd, set_OperFlavor, set_IEOperFlavor, set_OperDiagonal, set_OperTime:** [Requires manual description] (Operator generation routines for QMC moves.)
  - **FUNCTION check_EqualTime:** [Requires manual description]
  - **FUNCTION process_OperAdd, process_OperAdd_global:** [Requires manual description] (Process and time-order newly proposed operators.)
  - **SUBROUTINE insert_Oper, remove_Oper, clear_Trace:** [Requires manual description] (Modify the main operator list.)
  - **FUNCTION get_BosonicTrace:** [Requires manual description]
- **PROGRAM Prog_Trace:** [Requires manual description] (A test program included if `Trace_Test` is defined.)

# Important Variables/Constants

- **PMAX:** (Implicitly used from `MParameters`) Max dimension for Lanczos.
- **EPSLANC, EPSDEG:** (Implicitly used from `MParameters`) Tolerances.
- **Sector* constants:** (Implicitly used from `MParameters`) Worm sector definitions.
- **NOperWorm:** (Implicitly used from `MParameters`) Number of operators per worm sector.
[Requires manual identification and description of important variables/constants/common blocks]

# Usage Examples

[Requires manual addition of usage examples if applicable]

# Dependencies and Interactions

- **USE MParameters:** For kind parameters, constants, and parameter access.
- **USE MStates:** For state definitions (`TStates`, `TSubStates`).
- **USE MRandom:** For random number generation (`grnd`, `randint`).
- **USE MSparseMatrix:** For sparse matrix type (`TSparseMatrix`).
- **USE MLanczos:** For Lanczos time evolution routines.
- **USE MMatrixUpdate:** For matrix update routines (though some might be duplicated/specialized here).
- **USE MAusgabe:** For formatted printing in test programs.
- **USE MOperator:** For operator types and potentially some operator manipulation routines.
- **USE MCompoundIndex:** For `index2component_general`.
[Requires manual description of further interactions]
