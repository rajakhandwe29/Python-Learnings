# Modules and Packages in Python

## Modules

```python
# Import module
import math
print(math.pi)
print(math.sqrt(16))

# From import
from math import pi, sqrt
print(pi)

# Alias
import numpy as np
from collections import defaultdict as dd

# Create module (save as my_module.py)
# def greet(name):
#     return f"Hello, {name}!"

# Use module
import my_module
print(my_module.greet("Alice"))
```

## Packages

```
mypackage/
├── __init__.py
├── module1.py
├── module2.py
└── subpackage/
    ├── __init__.py
    └── module3.py
```

```python
# Import from package
from mypackage import module1
from mypackage.module2 import function_name
from mypackage.subpackage import module3

# Relative imports (within package)
# from . import module1
# from .subpackage import module3
```

## __init__.py

```python
# Make package importable
# Expose public API
from .module1 import public_function
from .module2 import AnotherClass

__all__ = ["public_function", "AnotherClass"]
```

## pip and Virtual Environments

```bash
# Create virtual environment
python -m venv venv

# Activate
source venv/bin/activate  # Linux/Mac
venv\Scripts\activate     # Windows

# Install packages
pip install requests
pip install -r requirements.txt

# Freeze dependencies
pip freeze > requirements.txt
```

## Best Practices

1. **Virtual environments** - One per project
2. **requirements.txt** - Document dependencies
3. **Meaningful names** - Clear module purpose
4. **Organize hierarchy** - Logical package structure
5. **Use __all__** - Define public API

---

**Next:** Explore advanced topics like threading and async!
