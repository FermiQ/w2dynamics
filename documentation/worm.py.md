# Overview

This file w2dyn/dmft/worm.py contains...
This module defines a mapping for "worm" sampling sectors in the CT-QMC algorithm and provides a function to determine the active worm sector based on configuration parameters. Worm sampling is a technique used in QMC to measure specific types of correlation functions or improved estimators efficiently.

# Key Components

- **get_sector_index:** [Requires manual description] (This function takes a configuration dictionary (`cfg`) as input, checks which `WormMeas...` parameters are enabled, and returns the corresponding integer index for the worm sampling sector. It also performs some validation checks, ensuring only one sector is active and that prerequisite configurations (like `FourPnt` for three-frequency objects) are set.)

# Important Variables/Constants

- **worms:** A dictionary that maps string keys (representing QMC configuration parameters for measuring specific quantities with the worm algorithm, e.g., `'WormMeasGiw'`, `'WormMeasG4iw'`) to integer values representing the corresponding worm sector index.
[Requires manual identification and description of important variables/constants]

# Usage Examples

[Requires manual addition of usage examples if applicable]
```python
# Example configuration (simplified)
config_qmc = {
    'WormMeasGiw': 0,
    'WormMeasGtau': 0,
    'WormMeasGSigmaiw': 0,
    'WormMeasG4iw': 1,  # Enable G4iw measurement
    'WormMeasH4iw': 0,
    # ... other WormMeas parameters ...
    'FourPnt': 8 # Required for G4iw
}

from w2dyn.dmft.worm import get_sector_index

try:
    sector = get_sector_index(config_qmc)
    print(f"Active worm sector: {sector}") # Expected output: 4
except ValueError as e:
    print(f"Configuration error: {e}")

```

# Dependencies and Interactions

- This module has no explicit Python import dependencies beyond standard library types.
- It is intended to be used by other modules that manage or configure the CT-QMC solver, likely within `w2dyn.dmft.impurity` (specifically `CtHybSolver`).
[Requires manual description of further interactions]
