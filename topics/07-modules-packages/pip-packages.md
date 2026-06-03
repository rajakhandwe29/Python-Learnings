# pip and Packages in Python

## Installing Packages

```bash
# Basic install
pip install requests

# Specific version
pip install django==3.2.0

# Upgrade package
pip install --upgrade numpy

# Install from requirements
pip install -r requirements.txt

# Create requirements file
pip freeze > requirements.txt
```

## Virtual Environments

```bash
# Create environment
python -m venv myenv

# Activate
source myenv/bin/activate  # Linux/Mac
myenv\Scripts\activate      # Windows

# Deactivate
deactivate

# Install in virtual env
pip install package_name
```

## Common Packages

```python
# Web
import requests  # HTTP library
import flask     # Web framework
import django    # Web framework

# Data
import pandas as pd  # Data manipulation
import numpy as np   # Numerical computing
import matplotlib    # Plotting

# Utilities
import dotenv        # Environment variables
import pyyaml        # YAML parsing
import click         # CLI creation
```

## Best Practices

1. **Always use virtual environments**
2. **Keep requirements.txt updated**
3. **Pin versions in production**
4. **Check package security** - Use bandit, safety
5. **Review dependencies** - Avoid bloat

---

**Next:** Create custom modules!
