# Error Handling in Python

## Overview

Error handling allows programs to gracefully manage exceptions and unexpected situations. It's essential for robust, production-ready code.

## Key Concepts

1. **Exceptions** - Built-in exception types and when they're raised
2. **Try-Except-Finally** - Standard error handling pattern
3. **Custom Exceptions** - Creating application-specific errors

## Quick Reference

```python
# Catch specific exception
try:
    operation()
except ValueError:
    handle_value_error()

# Multiple exceptions
try:
    operation()
except (ValueError, TypeError):
    handle_both()

# Any exception
try:
    operation()
except Exception as e:
    print(f"Error: {e}")

# Cleanup with finally
try:
    resource = open_resource()
except Error:
    handle_error()
finally:
    close_resource()
```

## Common Exceptions

| Exception | When Raised |
|-----------|------------|
| **ValueError** | Invalid value |
| **TypeError** | Wrong type |
| **IndexError** | Index out of range |
| **KeyError** | Key not found |
| **FileNotFoundError** | File missing |
| **ZeroDivisionError** | Divide by zero |
| **AttributeError** | Attribute missing |

## Best Practices

1. **Specific exceptions** - Catch what you expect
2. **Meaningful messages** - Help with debugging
3. **Use finally** - For cleanup
4. **Don't silence errors** - Log or re-raise
5. **Test error paths** - Verify handling works

---

**Next:** Organize code with modules and packages!
