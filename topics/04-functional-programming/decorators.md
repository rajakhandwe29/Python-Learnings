# Decorators in Python: A Comprehensive Guide

## Introduction

Decorators are functions that modify the behavior of other functions or classes without permanently changing their source code. They're a powerful feature that enables clean code and reusable enhancements.

## Basic Concept

```python
# Simple decorator
def my_decorator(func):
    def wrapper():
        print("Before function call")
        func()
        print("After function call")
    return wrapper

# Apply decorator using @
@my_decorator
def say_hello():
    print("Hello!")

say_hello()
# Output:
# Before function call
# Hello!
# After function call
```

## Decorators with Arguments

```python
def my_decorator(func):
    def wrapper(*args, **kwargs):
        print(f"Calling {func.__name__}")
        result = func(*args, **kwargs)
        print(f"Finished {func.__name__}")
        return result
    return wrapper

@my_decorator
def add(a, b):
    return a + b

result = add(5, 3)
print(result)  # Output: 8
```

## Decorator Factory Pattern

```python
def repeat(times):
    def decorator(func):
        def wrapper(*args, **kwargs):
            results = []
            for _ in range(times):
                results.append(func(*args, **kwargs))
            return results
        return wrapper
    return decorator

@repeat(3)
def get_random():
    import random
    return random.randint(1, 100)

print(get_random())  # Output: [42, 87, 23] (example)
```

## Common Decorators

### Logging Decorator
```python
def log_calls(func):
    def wrapper(*args, **kwargs):
        print(f"Calling: {func.__name__}({args}, {kwargs})")
        result = func(*args, **kwargs)
        print(f"Result: {result}")
        return result
    return wrapper

@log_calls
def multiply(a, b):
    return a * b

multiply(3, 4)
# Output:
# Calling: multiply((3, 4), {})
# Result: 12
```

### Timing Decorator
```python
import time

def timeit(func):
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        elapsed = time.time() - start
        print(f"{func.__name__} took {elapsed:.4f} seconds")
        return result
    return wrapper

@timeit
def slow_function():
    time.sleep(0.1)
    return "Done"

slow_function()
# Output: slow_function took 0.1003 seconds
```

### Caching Decorator
```python
def cache(func):
    cached_results = {}
    
    def wrapper(*args):
        if args not in cached_results:
            cached_results[args] = func(*args)
        return cached_results[args]
    
    return wrapper

@cache
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n-1) + fibonacci(n-2)

print(fibonacci(10))  # Computed efficiently with caching
```

## Multiple Decorators

```python
def decorator_a(func):
    def wrapper():
        print("A - Before")
        func()
        print("A - After")
    return wrapper

def decorator_b(func):
    def wrapper():
        print("B - Before")
        func()
        print("B - After")
    return wrapper

@decorator_a
@decorator_b
def my_function():
    print("Function called")

my_function()
# Output:
# A - Before
# B - Before
# Function called
# B - After
# A - After
```

## Class Decorators

```python
class CountCalls:
    def __init__(self, func):
        self.func = func
        self.count = 0
    
    def __call__(self, *args, **kwargs):
        self.count += 1
        print(f"Call #{self.count}")
        return self.func(*args, **kwargs)

@CountCalls
def say_hello():
    print("Hello!")

say_hello()  # Output: Call #1 / Hello!
say_hello()  # Output: Call #2 / Hello!
print(say_hello.count)  # Output: 2
```

## Decorating Classes

```python
def add_repr(cls):
    def __repr__(self):
        attrs = ", ".join(f"{k}={v}" for k, v in self.__dict__.items())
        return f"{cls.__name__}({attrs})"
    
    cls.__repr__ = __repr__
    return cls

@add_repr
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

person = Person("Alice", 30)
print(person)  # Output: Person(name=Alice, age=30)
```

## Using functools.wraps

```python
import functools

def my_decorator(func):
    @functools.wraps(func)  # Preserves original function metadata
    def wrapper(*args, **kwargs):
        """Wrapper function"""
        return func(*args, **kwargs)
    return wrapper

@my_decorator
def add(a, b):
    """Add two numbers"""
    return a + b

print(add.__name__)   # Output: add (not wrapper)
print(add.__doc__)    # Output: Add two numbers
```

## Practical Examples

### Authentication Decorator
```python
def require_auth(func):
    def wrapper(*args, **kwargs):
        user = kwargs.get('user')
        if not user or not user.get('authenticated'):
            raise ValueError("Not authenticated")
        return func(*args, **kwargs)
    return wrapper

@require_auth
def get_user_data(user_id, user=None):
    return f"Data for user {user_id}"

# Usage
user = {'authenticated': True}
print(get_user_data(123, user=user))  # Works

# user = {'authenticated': False}
# get_user_data(123, user=user)  # Raises ValueError
```

### Rate Limiting Decorator
```python
import time

def rate_limit(max_calls, time_window):
    def decorator(func):
        calls = []
        
        def wrapper(*args, **kwargs):
            now = time.time()
            # Remove old calls outside time window
            calls[:] = [c for c in calls if c > now - time_window]
            
            if len(calls) >= max_calls:
                raise ValueError("Rate limit exceeded")
            
            calls.append(now)
            return func(*args, **kwargs)
        
        return wrapper
    return decorator

@rate_limit(max_calls=3, time_window=10)
def api_call():
    return "Response"

# Can call 3 times in 10 seconds
for i in range(3):
    print(api_call())

# try:
#     api_call()  # Raises ValueError
# except ValueError as e:
#     print(e)
```

## Best Practices

### 1. Preserve Function Metadata
```python
import functools

# GOOD - use @functools.wraps
def my_decorator(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        return func(*args, **kwargs)
    return wrapper

# BAD - metadata lost
def bad_decorator(func):
    def wrapper(*args, **kwargs):
        return func(*args, **kwargs)
    return wrapper
```

### 2. Keep Decorators Simple
```python
# GOOD - focused decorator
def log_result(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        result = func(*args, **kwargs)
        print(f"Result: {result}")
        return result
    return wrapper

# BAD - does too much
def complex_decorator(func):
    # Logging, caching, validation all mixed together
    pass
```

### 3. Document Decorators
```python
def retry(max_attempts=3):
    """Retry decorator - retries function call on exception.
    
    Args:
        max_attempts: Maximum number of retry attempts
    
    Returns:
        Decorated function
    """
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            for attempt in range(max_attempts):
                try:
                    return func(*args, **kwargs)
                except Exception as e:
                    if attempt == max_attempts - 1:
                        raise
        return wrapper
    return decorator
```

## Summary

| Type | Purpose | Example |
|------|---------|---------|
| **Simple** | Wrap function | `@decorator` |
| **Factory** | Configurable | `@decorator(config)` |
| **Class** | Stateful | `class Decorator` |
| **Chained** | Multiple wrappers | `@decorator1 @decorator2` |

### Key Takeaways

1. **Decorators wrap functions** - adding behavior without modifying original
2. **Use @functools.wraps** - preserves function metadata
3. **Decorators are functions** - they return functions
4. **Factory pattern** - create configurable decorators
5. **Keep them focused** - single responsibility
6. **Document behavior** - what does decorator add?
7. **Common use cases** - logging, caching, validation, timing

### Practice Exercises

1. Create a logging decorator
2. Build a caching decorator
3. Implement a rate limiting decorator
4. Create a retry decorator with exponential backoff
5. Build a validation decorator

---

**Next:** Learn generators for memory-efficient iteration!
