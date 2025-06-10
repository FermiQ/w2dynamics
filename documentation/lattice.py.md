# Overview

This file w2dyn/dmft/lattice.py contains...
This module defines classes for representing different types of lattice models used in DMFT. The core idea is to abstract the way the self-energy is incorporated into the Dyson equation to obtain the local Green's function.

Key classes include:
- `Lattice`: An abstract base class defining the interface for lattice models. It handles basic properties like temperature (`beta`), number of orbitals, and spins. It declares methods for computing the density of states (`compute_dos`), the local Green's function (`gloc`), a model Green's function (`gmodel`), and traces of the Green's function (`trace`).
- `KspaceHamiltonian`: Implements a lattice defined by a k-space Hamiltonian `H(k)`. It performs k-summations to calculate `gloc`. It also includes a nested `EVTraceFactory` for more efficient computation of traces by changing to an eigenbasis.
- `Bethe`: Represents a lattice with a semi-elliptic density of states (Bethe lattice).
- `DensityOfStates`: Represents a lattice defined by a user-provided density of states.
- `NanoLattice`: A subclass of `KspaceHamiltonian`, likely specialized for nanostructure calculations, incorporating leads and their hybridization functions.

Helper functions like `fermi` (Fermi-Dirac distribution) and `rmap` (reverse mapping) are also provided.

# Key Components

- **fermi:** [Requires manual description] (Module-level function)
- **dfermi:** [Requires manual description] (Module-level function)
- **rmap:** [Requires manual description] (Module-level function)
- **Lattice:** [Requires manual description] (Abstract Base Class)
  - **__init__:** [Requires manual description]
  - **compute_dos:** [Requires manual description] (Abstract)
  - **gloc:** [Requires manual description] (Abstract)
  - **gmodel:** [Requires manual description]
  - **trace:** [Requires manual description]
  - **TraceFactory:** [Requires manual description] (Nested class for `trace`)
    - **__init__:** [Requires manual description]
    - **trgloc:** [Requires manual description]
    - **trgmodel:** [Requires manual description]
  - **_model_integrate:** [Requires manual description] (Helper)
- **KspaceHamiltonian:** [Requires manual description] (Derived from `Lattice`)
  - **__init__:** [Requires manual description]
  - **compute_dos:** [Requires manual description]
  - **gloc:** [Requires manual description]
  - **trace:** [Requires manual description] (Overrides base to potentially use `EVTraceFactory`)
  - **EVTraceFactory:** [Requires manual description] (Nested class, derived from `Lattice.TraceFactory`)
    - **get_eigvals:** [Requires manual description]
    - **__init__:** [Requires manual description]
    - **trgloc:** [Requires manual description]
- **Bethe:** [Requires manual description] (Derived from `Lattice`)
  - **_get_dos:** [Requires manual description]
  - **__init__:** [Requires manual description]
  - **compute_dos:** [Requires manual description]
  - **gloc:** [Requires manual description]
- **DensityOfStates:** [Requires manual description] (Derived from `Lattice`)
  - **get_dos_bethe:** [Requires manual description] (Static method)
  - **__init__:** [Requires manual description]
  - **compute_dos:** [Requires manual description]
  - **gloc:** [Requires manual description]
- **NanoLattice:** [Requires manual description] (Derived from `KspaceHamiltonian`)
  - **get_leadsiw:** [Requires manual description]
  - **__init__:** [Requires manual description]
  - **compute_dos:** [Requires manual description]
  - **gloc:** [Requires manual description]
  - **trace:** [Requires manual description]
  - **_get_leadsiw:** [Requires manual description] (Helper)

# Important Variables/Constants

[Requires manual identification and description of important variables/constants]

# Usage Examples

[Requires manual addition of usage examples if applicable]

# Dependencies and Interactions

- **numpy:** Imported as `np`.
- **scipy.ndimage:** Imported by this file (specifically `scipy.ndimage.filters.gaussian_filter1d`).
- **scipy.signal:** Imported by this file (not visibly used in the snippet).
- **scipy.optimize:** Imported by this file (used for `brentq`).
- **scipy.integrate:** Imported by this file (used for `trapz`, `cumtrapz`).
- **warnings:** Specifically `warn` is used.
- **w2dyn.auxiliaries.transform:** Imported as `tr`.
- **w2dyn.dmft._compat:** Imported as `_linalg` (provides compatibility for linear algebra functions).
- **w2dyn.dmft.orbspin:** Imported as `orbspin`.
- **copy:** Imported by this file.
[Requires manual description of further interactions]
