# Overview

This file w2dyn/dmft/mixing.py contains...
This module provides classes for implementing various mixing strategies to accelerate the convergence of self-consistent field (SCF) iterations, such as those in a DMFT loop. Mixing involves combining previous results with new calculations to generate a better trial input for the next iteration.

The module offers several mixer classes:
- `NoMixingMixer`: A pass-through mixer that performs no mixing.
- `LinearMixer`: Implements simple linear mixing, where a share of the previous iteration's output is mixed with the new output.
- `DiisMixer`: Implements Pulay mixing (also known as Direct Inversion in the Iterative Subspace - DIIS), which uses a history of trial inputs and their corresponding residuals to extrapolate a better next trial.

It also includes decorator classes to modify the behavior of other mixers:
- `InitialMixingDecorator`: Allows using one mixer for an initial number of iterations and then switching to another.
- `FlatMixingDecorator`: Flattens nested list/array structures before passing them to the decorated mixer and restores the original shape afterward.
- `RealMixingDecorator`: Separates the real and imaginary parts of complex arrays, passes them to the decorated mixer, and then recombines them.

# Key Components

- **InitialMixingDecorator:** [Requires manual description]
  - **__init__:** [Requires manual description]
  - **__call__:** [Requires manual description]
- **FlatMixingDecorator:** [Requires manual description]
  - **__init__:** [Requires manual description]
  - **__call__:** [Requires manual description]
- **RealMixingDecorator:** [Requires manual description]
  - **__init__:** [Requires manual description]
  - **__call__:** [Requires manual description]
- **NoMixingMixer:** [Requires manual description]
  - **__call__:** [Requires manual description]
- **LinearMixer:** [Requires manual description]
  - **__init__:** [Requires manual description]
  - **__call__:** [Requires manual description]
- **DiisMixer:** [Requires manual description]
  - **__init__:** [Requires manual description]
  - **__call__:** [Requires manual description]

# Important Variables/Constants

[Requires manual identification and description of important variables/constants]

# Usage Examples

[Requires manual addition of usage examples if applicable]

# Dependencies and Interactions

- **numpy:** Imported as `np`.
- **w2dyn.auxiliaries.deepflatten:** Imported as `deepflatten` (used by `FlatMixingDecorator`).
[Requires manual description of further interactions]
