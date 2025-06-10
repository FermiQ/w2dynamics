# Overview

This file w2dyn/dmft/_compat.py contains...
This module provides compatibility functions for different versions of NumPy. It aims to ensure that the w2dynamics code can run correctly even with older NumPy versions by providing workarounds or custom implementations for features that might be missing or behave differently.

# Key Components

- **diagonal:** [Requires manual description] (A wrapper around `numpy.diagonal` to handle zero-size arrays correctly.)
- **fromiter:** [Requires manual description] (A generalization of `numpy.fromiter` to support multi-dimensional arrays and better error reporting for older NumPy versions.)
- **inv:** [Requires manual description] (An alias for `numpy.linalg.inv` if NumPy version is >= 1.8, otherwise a custom implementation that applies `numpy.linalg.inv` over the last two dimensions of a potentially higher-dimensional array.)
- **eigvals:** [Requires manual description] (An alias for `numpy.linalg.eigvals` if NumPy version is >= 1.8, otherwise a custom implementation that applies `numpy.linalg.eigvals` over the last two dimensions.)
- **eigh:** [Requires manual description] (An alias for `numpy.linalg.eigh` if NumPy version is >= 1.8, otherwise a custom implementation that applies `numpy.linalg.eigh` over the last two dimensions.)

# Important Variables/Constants

- **numpy_version:** A tuple representing the currently installed NumPy version (e.g., `(1, 18, 5)`). This is used to conditionally define functions.
[Requires manual identification and description of important variables/constants]

# Usage Examples

[Requires manual addition of usage examples if applicable]

# Dependencies and Interactions

- **warnings:** Specifically `warn` is used to notify the user if emulated functions are being used due to an older NumPy version.
- **numpy:** Imported as `np`. Core functionalities and `numpy.linalg` are used.
[Requires manual description of further interactions]
