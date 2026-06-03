# Modules and Packages

## Overview

Modules and packages are the foundation of Python code organization. They enable code reuse, maintainability, and scalability.

## Concepts

1. **Modules** - Single .py files with code
2. **Packages** - Directories with __init__.py
3. **Imports** - Various import styles
4. **pip** - Package manager for Python

## Quick Reference

```python
# Import module
import json

# From import
from pathlib import Path

# Alias
import numpy as np

# All imports
from utils import *

# Relative import (in package)
from .module import function
```

## Project Structure

```
project/
├── venv/
├── requirements.txt
├── main.py
└── mypackage/
    ├── __init__.py
    └── utils.py
```

## Key Topics

- **Imports** - Various import mechanisms
- **pip & Packages** - Package management
- **Creating Modules** - Build reusable code

## Best Practices

1. **Virtual environments** - Isolate dependencies
2. **requirements.txt** - Document dependencies
3. **Clear structure** - Organize logically
4. **Docstrings** - Document modules
5. **__all__** - Define public API

---

Ready for advanced topics!
