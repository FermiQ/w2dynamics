# Overview

This file w2dyn/dmft/selfcons.py contains...
This module defines the core logic for the DMFT self-consistency loop. It brings together components like the lattice definition, impurity problem solvers, double-counting schemes, and mixing strategies to iteratively find a self-consistent solution.

Key classes and functions:
- `iw_to_tau_fast`: A utility function for performing a fast Fourier transform from Matsubara frequencies to imaginary time.
- `FrequencyDistribution`: A helper class to manage the distribution of frequency points across MPI ranks, enabling parallel computation over frequencies.
- `DMFTStep`: The central class orchestrating a single DMFT iteration. It handles:
    - Setting up the self-energy (including mixing and double-counting).
    - Updating the chemical potential to match a target density.
    - Calculating the local Green's function (`gloc`) using the lattice model and the current self-energy.
    - Constructing the Weiss field (`g0inv`) and hybridization function (`fiw`, `ftau`) for the next impurity problem.
    - Interfacing with impurity solvers.
    - Writing output data.
- `KappaMuExtrapolator`: A helper class for extrapolating the chemical potential (`mu`) based on previous iterations' densities and `mu` values, aiming to accelerate convergence to the target density. It uses an estimate of the compressibility (`kappa`).

# Key Components

- **iw_to_tau_fast:** [Requires manual description] (Module-level utility function.)
- **FrequencyDistribution:** [Requires manual description]
  - **__init__:** [Requires manual description]
  - **rdebug:** [Requires manual description]
  - **set_niw:** [Requires manual description]
  - **allgather:** [Requires manual description]
  - **shape:** [Requires manual description]
  - **parts:** [Requires manual description]
- **DMFTStep:** [Requires manual description]
  - **__init__:** [Requires manual description]
  - **set_siws:** [Requires manual description] (Sets/updates the self-energies and double counting.)
  - **update_mu:** [Requires manual description] (Adjusts chemical potential to reach target density.)
  - **set_mu:** [Requires manual description]
  - **siw2gloc:** [Requires manual description] (Calculates `gloc` from `siw`.)
  - **write_gloc:** [Requires manual description]
  - **write_before_mu_search:** [Requires manual description]
  - **write_lattice_problem:** [Requires manual description]
  - **gloc2fiw:** [Requires manual description] (Calculates Weiss field and hybridization for the impurity problem.)
  - **write_imp_problems:** [Requires manual description]
- **KappaMuExtrapolator:** [Requires manual description]
  - **__init__:** [Requires manual description]
  - **initialize:** [Requires manual description]
  - **has_mu:** [Requires manual description]
  - **next_mu:** [Requires manual description]
  - **step:** [Requires manual description]

# Important Variables/Constants

[Requires manual identification and description of important variables/constants]

# Usage Examples

[Requires manual addition of usage examples if applicable]

# Dependencies and Interactions

- **warnings:** Specifically `warn` is used.
- **numpy:** Imported as `np`.
- **scipy.optimize:** Imported as `opt` (used for `brentq` in chemical potential search).
- **sys:** Imported by this file.
- **w2dyn.dmft.impurity:** Imported as `impurity`.
- **w2dyn.dmft.doublecounting:** Imported as `doublecounting`.
- **w2dyn.dmft.orbspin:** Imported as `orbspin`.
- **w2dyn.dmft.gw:** Imported as `gw` (Note: `gw` module is currently non-functional).
- **w2dyn.dmft.mixing:** Imported as `mixing`.
- **w2dyn.auxiliaries.transform:** Imported as `tf`.
- Interacts heavily with `Lattice` objects (though not directly imported, it's passed to `DMFTStep`).
- Uses MPI via `mpi_comm` passed to `DMFTStep` and used by `FrequencyDistribution`.
[Requires manual description of further interactions]
