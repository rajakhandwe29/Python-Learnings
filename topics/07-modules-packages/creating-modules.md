# Creating Modules and Packages

## Simple Module

```python
# my_math.py
def add(a, b):
    """Add two numbers"""
    return a + b

def subtract(a, b):
    """Subtract two numbers"""
    return a - b

class Calculator:
    """Simple calculator class"""
    def multiply(self, a, b):
        return a * b

# Usage
import my_math
print(my_math.add(5, 3))
```

## Package Structure

```
my_package/
├── __init__.py
├── utils.py
├── database.py
└── api.py
```

```python
# __init__.py
from .utils import helper_function
from .database import Database

__version__ = "1.0.0"
__all__ = ["helper_function", "Database"]

# Usage
from my_package import Database
db = Database()
```

## Module Best Practices

1. **Clear names** - Module name reflects purpose
2. **Docstrings** - Document module purpose
3. **Organization** - Logical structure
4. **Exports** - Use __all__ for API

---

Next: Advanced topics!
