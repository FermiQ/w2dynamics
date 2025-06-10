# Overview

This file src/ctqmc_fortran/CTQMC.F90 contains...
This Fortran module, `MCTQMC`, is the core of the Continuous-Time Quantum Monte Carlo (CT-QMC) simulation. It orchestrates the QMC steps, including initialization, warm-up, measurements, and updates (like adding/removing operators, global moves, worm algorithm moves). It manages various physical quantities such as Green's functions in imaginary time (`Gtau`) and Matsubara frequencies (`Giw`), self-energies, two-particle and four-particle Green's functions, occupation numbers, and histograms. The module also handles different measurement techniques, including standard sampling in the Z-space (partition function) and various worm sampling sectors for improved estimators or specific correlation functions. It interacts with other modules for parameters, operator definitions, trace calculations, state management, random number generation, Fourier transforms, and signal handling.

# Key Components

- **MODULE MCTQMC:** [Requires manual description]
  - **SUBROUTINE wasted:** [Requires manual description] (Interface to a C function, likely for timing, used if `USE_REALTIME` is defined.)
  - **SUBROUTINE init_CTQMC:** [Requires manual description] (Initializes QMC parameters, allocates arrays for various measured quantities, and sets up common FT parameters.)
  - **SUBROUTINE init_counters:** [Requires manual description] (Resets various acceptance and try counters for QMC moves.)
  - **SUBROUTINE dest_CTQMC:** [Requires manual description] (Deallocates all dynamically allocated arrays used in the QMC simulation.)
  - **SUBROUTINE measure_giw_nfft:** [Requires manual description] (Measures G(iw) using NFFT if enabled.)
  - **SUBROUTINE measure_giw_worm:** [Requires manual description] (Measures G(iw) in worm space.)
  - **SUBROUTINE measure_gtau_worm:** [Requires manual description] (Measures G(tau) in worm space.)
  - **SUBROUTINE measure_ie_sigma_worm:** [Requires manual description] (Measures improved estimator for Sigma in worm space.)
  - **SUBROUTINE measure_quddag_worm:** [Requires manual description] (Measures Q U Ddag quantity in worm space.)
  - **SUBROUTINE measure_qq_worm:** [Requires manual description] (Measures QQ improved estimator in worm space.)
  - **SUBROUTINE measure_qqtau_worm:** [Requires manual description] (Measures QQ in tau bins in worm space.)
  - **SUBROUTINE measure_p2iw_worm:** [Requires manual description] (Measures 2-leg, 2-particle GF (PH) in worm space.)
  - **SUBROUTINE measure_p2tau_worm:** [Requires manual description] (Measures 2-leg, 2-particle GF (PH, tau) in worm space.)
  - **SUBROUTINE measure_p2iwpp_worm:** [Requires manual description] (Measures 2-leg, 2-particle GF (PP) in worm space.)
  - **SUBROUTINE measure_p2taupp_worm:** [Requires manual description] (Measures 2-leg, 2-particle GF (PP, tau) in worm space.)
  - **SUBROUTINE measure_p3iw_worm:** [Requires manual description] (Measures 3-leg, 2-particle GF (PH) in worm space.)
  - **SUBROUTINE measure_p3iwpp_worm:** [Requires manual description] (Measures 3-leg, 2-particle GF (PP) in worm space.)
  - **SUBROUTINE measure_g4iw_worm_nfft2d:** [Requires manual description] (Measures G4(iw) using 2D NFFT slices in worm space.)
  - **SUBROUTINE measure_g4iw_worm:** [Requires manual description] (Measures G4(iw) using 3D NFFT in worm space.)
  - **SUBROUTINE measure_ie_chi_worm:** [Requires manual description] (Measures improved estimator for Chi in worm space.)
  - **SUBROUTINE measure_qqqq_worm:** [Requires manual description] (Measures QQQQ improved estimator in worm space.)
  - **SUBROUTINE measure_nqqdag_worm:** [Requires manual description] (Measures NQQdag improved estimator in worm space.)
  - **SUBROUTINE measure_qqdd_worm:** [Requires manual description] (Measures QQdd improved estimator in worm space.)
  - **SUBROUTINE measure_ucaca_worm:** [Requires manual description]
  - **SUBROUTINE measure_ucacatau_worm:** [Requires manual description]
  - **SUBROUTINE measure_uccaa_worm:** [Requires manual description]
  - **SUBROUTINE measure_uccaatau_worm:** [Requires manual description]
  - **SUBROUTINE measure_g4iw_nfft:** [Requires manual description] (Measures G4(iw) using NFFT in Z-space.)
  - **SUBROUTINE MeasGtauRem:** [Requires manual description] (Measures G(tau) by removing operators.)
  - **SUBROUTINE MeasGiwFlushLookup:** [Requires manual description] (Flushes G(iw) lookup table for NFFT.)
  - **SUBROUTINE MeasGtauRem_full:** [Requires manual description] (Measures full off-diagonal G(tau).)
  - **SUBROUTINE MeasGtau4PntLeg:** [Requires manual description] (Measures G4 in mixed Legendre/Matsubara basis.)
  - **SUBROUTINE create_ssquare_full:** [Requires manual description] (Creates the S^2 operator matrix.)
  - **SUBROUTINE MeasureS2_from_densitymatrix:** [Requires manual description] (Measures <S^2> from the density matrix.)
  - **SUBROUTINE MeasSingleOcc_from_Densitymatrix:** [Requires manual description]
  - **SUBROUTINE MeasDoubleOcc_from_Densitymatrix:** [Requires manual description]
  - **SUBROUTINE Meas_rho2_from_Densitymatrix:** [Requires manual description] (Measures two-particle density matrix.)
  - **SUBROUTINE Meas_rho1_from_Densitymatrix:** [Requires manual description] (Measures one-particle density matrix.)
  - **SUBROUTINE MeasDensityMatrix_beta_half:** [Requires manual description] (Measures density matrix at beta/2.)
  - **SUBROUTINE MeasSusz:** [Requires manual description] (Measures Sz(tau)Sz(0) like quantities.)
  - **SUBROUTINE Transform_DensityMatrix_EB_to_OCCB:** [Requires manual description] (Transforms density matrix from eigenbasis to occupation basis.)
  - **SUBROUTINE MeasExpResDensityMatrix:** [Requires manual description] (Measures expansion order resolved density matrix.)
  - **SUBROUTINE MeasExpOrder:** [Requires manual description] (Measures histogram of expansion orders.)
  - **SUBROUTINE MeasOuterHistograms:** [Requires manual description] (Measures histograms related to outer states/superstates.)
  - **SUBROUTINE MeasSign:** [Requires manual description] (Measures the average sign.)
  - **SUBROUTINE StepAdd:** [Requires manual description] (Proposes and accepts/rejects adding a pair of hybridization operators.)
  - **SUBROUTINE StepAdd4:** [Requires manual description] (Proposes and accepts/rejects adding two pairs of hybridization operators.)
  - **SUBROUTINE StepRem:** [Requires manual description] (Proposes and accepts/rejects removing a pair of hybridization operators.)
  - **SUBROUTINE StepRem4:** [Requires manual description] (Proposes and accepts/rejects removing two pairs of hybridization operators.)
  - **SUBROUTINE StepGlob:** [Requires manual description] (Performs global QMC moves like spin flips or permutations.)
  - **SUBROUTINE StepShiftTau:** [Requires manual description] (Shifts all operator times or changes outer state if trace is empty.)
  - **SUBROUTINE StepChangeOuter:** [Requires manual description] (Changes the outer state when the trace is empty.)
  - **SUBROUTINE StepShiftTau_proper:** [Requires manual description] (Shifts all operator times when trace is not empty.)
  - **SUBROUTINE StepFlavourchange_general:** [Requires manual description] (Changes the flavour of a pair of operators.)
  - **SUBROUTINE StepWormAdd:** [Requires manual description] (Adds worm operators.)
  - **SUBROUTINE StepWormRem:** [Requires manual description] (Removes worm operators.)
  - **SUBROUTINE StepWormHybAdd:** [Requires manual description] (Adds a mix of worm and hybridization operators.)
  - **SUBROUTINE StepWormHybRem:** [Requires manual description] (Removes a mix of worm and hybridization operators.)
  - **SUBROUTINE get_Proposal:** [Requires manual description] (Calculates proposal probabilities for worm moves.)
  - **SUBROUTINE StepWormReplace:** [Requires manual description] (Replaces a worm operator with a hybridization operator or vice-versa.)
  - **SUBROUTINE count_steps:** [Requires manual description] (Counts steps in Z and Worm space for eta search.)
  - **SUBROUTINE findEta:** [Requires manual description] (Finds optimal eta for worm sampling.)
  - **FUNCTION equal_large:** [Requires manual description] (Compares two large numbers.)
  - **SUBROUTINE StepAdd_mine, StepRem_mine, MeasOcc_seg, MeasSusz_seg, StepGlob_mine:** [Requires manual description] (Segment algorithm specific versions of QMC moves and measurements.)
  - **SUBROUTINE init_solver:** [Requires manual description] (Initializes the solver with problem parameters.)
  - **SUBROUTINE ctqmc_calibrate:** [Requires manual description] (Calibrates window for tau shift moves.)
  - **SUBROUTINE set_taudiffmax:** [Requires manual description]
  - **SUBROUTINE ctqmc_warmup:** [Requires manual description] (Performs QMC warm-up steps.)
  - **SUBROUTINE ctqmc_worm_warmup:** [Requires manual description] (Performs QMC warm-up for worm sampling.)
  - **SUBROUTINE ctqmc_measure:** [Requires manual description] (Main QMC measurement loop.)
  - **SUBROUTINE get_mc_config_scalars, get_mc_config, set_mc_config, set_empty_mc_config:** [Requires manual description] (Routines for getting/setting Monte Carlo configurations for restart.)
  - **SUBROUTINE init_rnd, init_paras, dest_paras:** [Requires manual description] (Interface routines for random number generator and parameter handling.)
  - **SUBROUTINE invFT, FT, FlatHybr, SemiCircHybr, get_gbethe_para, get_gsumhk_para, get_Gk, get_Polarization, get_DOS, get_fiwflat, get_fiwsemi, Linrg_cmplx, inverse, eigvals_cmplx:** [Requires manual description] (Various physics/math utility functions, some possibly deprecated or for specific test cases.)
- **PROGRAM Prog_CTQMC:** [Requires manual description] (A test program included if `CTQMC_Test` is defined.)

# Important Variables/Constants

- Numerous module-level allocatable arrays for storing QMC results (e.g., `Gtau`, `Giw`, `G4iw`, `occ`, `Histo`).
- Parameters controlling QMC moves (e.g., `PercentageGlobalMove`, `PercentageWormInsert`).
- Constants for FourPnt GF measurement modes (e.g., `GF4_IMAGTIME`, `GF4_LEGENDRE`).
[Requires manual identification and description of important variables/constants/common blocks]

# Usage Examples

[Requires manual addition of usage examples if applicable]

# Dependencies and Interactions

- **USE MParameters:** For kind parameters.
- **USE MOperator, MTrace, MStates, MRandom, MAngularMomentum, LegendrePoly, type_progress, signals, MAusgabe, ft_worm:** Various local modules for core QMC components.
- **USE ft_fast / ft_naive:** Conditional use for Fourier transforms (NFFT or naive).
- **USE iso_c_binding:** For C interoperability.
- **USE ft_common:** For common Fourier transform parameters.
[Requires manual description of further interactions]
