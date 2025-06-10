# Overview

This file w2dyn/dmft/meta.py contains...
This file primarily defines a large dictionary named `QUANTITIES`. This dictionary serves as a metadata store for various physical quantities that are used or produced within the w2dynamics code. For each quantity (keyed by a string name), it stores information such as:
- `axes`: A list of strings describing the dimensions/axes of the quantity (e.g., "ineq", "band", "spin", "iw").
- `desc`: A textual description of the quantity.

This metadata is likely used elsewhere in the codebase, for example, when reading/writing HDF5 files to understand the structure and meaning of datasets, or for generating documentation or user interfaces.

# Key Components

- **QUANTITIES:** [Requires manual description] (A large dictionary holding metadata for various physical quantities.)

# Important Variables/Constants

- **QUANTITIES:** As described above, this is the main constant defined in this file.
[Requires manual identification and description of important variables/constants]

# Usage Examples

[Requires manual addition of usage examples if applicable]
This file itself is not executable but provides a data structure used by other modules. An example of how another module might use it:
```python
from w2dyn.dmft.meta import QUANTITIES

# Get metadata for the 'siw-full' quantity
siw_metadata = QUANTITIES.get("siw-full")
if siw_metadata:
    print(f"Description: {siw_metadata['desc']}")
    print(f"Axes: {siw_metadata['axes']}")
```

# Dependencies and Interactions

- **textwrap:** Specifically `dedent` is imported (used for formatting multi-line descriptions in the `QUANTITIES` dictionary).
- This module is primarily a data definition module. Other modules in `w2dyn` likely import and use the `QUANTITIES` dictionary.
[Requires manual description of further interactions]
