# Exception Handling in Python: A Comprehensive Guide

## Built-in Exceptions

```python
# Most common exceptions:
# ValueError - invalid value
try:
    int("not_a_number")
except ValueError as e:
    print(f"Error: {e}")

# TypeError - wrong type
try:
    5 + "string"
except TypeError as e:
    print(f"Error: {e}")

# IndexError - list index out of range
try:
    lst = [1, 2, 3]
    print(lst[10])
except IndexError:
    print("Index out of range")

# KeyError - dictionary key not found
try:
    d = {"a": 1}
    print(d["b"])
except KeyError:
    print("Key not found")

# FileNotFoundError - file doesn't exist
try:
    with open("nonexistent.txt") as f:
        content = f.read()
except FileNotFoundError:
    print("File not found")

# ZeroDivisionError - division by zero
try:
    result = 10 / 0
except ZeroDivisionError:
    print("Cannot divide by zero")

# AttributeError - attribute doesn't exist
try:
    "string".nonexistent_method()
except AttributeError:
    print("Attribute not found")
```

## Try-Except Blocks

```python
# Basic try-except
try:
    risky_operation()
except SomeException:
    handle_error()

# Multiple exceptions
try:
    operation()
except (ValueError, TypeError) as e:
    print(f"Error: {e}")

# Different handlers for different exceptions
try:
    operation()
except ValueError:
    handle_value_error()
except TypeError:
    handle_type_error()
except Exception as e:  # Catch-all
    handle_generic_error(e)

# Accessing exception info
try:
    int("invalid")
except ValueError as e:
    print(f"Exception type: {type(e)}")
    print(f"Message: {str(e)}")
    import traceback
    traceback.print_exc()
```

## Finally and Else

```python
# Finally - always executes
try:
    file = open("file.txt")
    content = file.read()
except FileNotFoundError:
    print("File not found")
finally:
    file.close()  # Always closes

# Else - executes if no exception
try:
    result = risky_operation()
except Exception:
    print("Error occurred")
else:
    print("Success:", result)  # Only if no exception

# Complete example
try:
    data = validate_data()
except ValueError as e:
    print(f"Validation error: {e}")
except Exception as e:
    print(f"Unexpected error: {e}")
else:
    process_data(data)
finally:
    cleanup()
```

## Raising Exceptions

```python
# Raise built-in exception
def validate_age(age):
    if age < 0:
        raise ValueError("Age cannot be negative")
    if age > 150:
        raise ValueError("Age unreasonable")
    return age

try:
    validate_age(-5)
except ValueError as e:
    print(f"Invalid age: {e}")

# Re-raise exceptions
try:
    operation()
except Exception as e:
    print("Error occurred")
    raise  # Re-raise the same exception
```

## Summary

| Exception | When Raised |
|-----------|------------|
| **ValueError** | Invalid value for a type |
| **TypeError** | Wrong data type |
| **IndexError** | List index out of range |
| **KeyError** | Dictionary key not found |
| **FileNotFoundError** | File doesn't exist |
| **AttributeError** | Attribute doesn't exist |
| **ZeroDivisionError** | Division by zero |
| **ImportError** | Cannot import module |

### Key Takeaways

1. **Use specific exceptions** - Catch what you expect
2. **Handle or propagate** - Don't ignore errors silently
3. **Use finally for cleanup** - Ensure resources are freed
4. **Meaningful messages** - Help debugging
5. **Test error cases** - Verify error handling works

---

**Next:** Learn custom exceptions for application-specific errors!
