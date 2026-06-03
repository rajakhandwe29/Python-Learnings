# Custom Exceptions in Python

## Creating Custom Exceptions

```python
# Simple custom exception
class CustomError(Exception):
    pass

try:
    raise CustomError("Something went wrong")
except CustomError as e:
    print(f"Caught custom error: {e}")

# Custom exception with additional info
class ValidationError(Exception):
    def __init__(self, message, field=None):
        self.message = message
        self.field = field
        super().__init__(self.message)
    
    def __str__(self):
        if self.field:
            return f"Validation error in {self.field}: {self.message}"
        return self.message

# Usage
def validate_email(email):
    if "@" not in email:
        raise ValidationError("Invalid email format", field="email")
    return email

try:
    validate_email("invalid_email")
except ValidationError as e:
    print(e)
```

## Exception Hierarchies

```python
# Create exception hierarchy
class ApplicationError(Exception):
    """Base exception for application"""
    pass

class DatabaseError(ApplicationError):
    """Database-related errors"""
    pass

class ValidationError(ApplicationError):
    """Validation errors"""
    pass

class ConfigurationError(ApplicationError):
    """Configuration errors"""
    pass

# Usage
try:
    raise DatabaseError("Connection failed")
except DatabaseError as e:
    print(f"DB Error: {e}")
except ApplicationError as e:
    print(f"Application Error: {e}")
```

## Best Practices

1. **Inherit from Exception** - Always inherit properly
2. **Meaningful names** - Clear error type from name
3. **Useful messages** - Help debugging
4. **Hierarchy** - Organize related exceptions
5. **Document** - Explain when each exception is raised

---

**Next:** Learn modules and packages for code organization!
