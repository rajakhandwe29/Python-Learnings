# Functions

Learn to write reusable, modular code with functions.

## Table of Contents
1. [Function Basics](#function-basics)
2. [Parameters and Arguments](#parameters-and-arguments)
3. [Return Values](#return-values)
4. [Scope](#scope)
5. [Advanced Functions](#advanced-functions)

---

## Function Basics

### What is a Function?

A function is a reusable block of code that performs a specific task.

```python
# Define a function
def greet():
    print("Hello, World!")

# Call the function
greet()

# Output: Hello, World!
```

### Function with Parameters

```python
# Define function with parameters
def greet(name):
    print(f"Hello, {name}!")

# Call with arguments
greet("Alice")      # Hello, Alice!
greet("Bob")        # Hello, Bob!

# Multiple parameters
def add(a, b):
    print(f"{a} + {b} = {a + b}")

add(5, 3)           # 5 + 3 = 8
```

### Function Documentation (Docstrings)

```python
def calculate_area(length, width):
    """
    Calculate the area of a rectangle.
    
    Args:
        length (float): The length of the rectangle
        width (float): The width of the rectangle
    
    Returns:
        float: The area of the rectangle
    
    Example:
        >>> calculate_area(5, 3)
        15
    """
    return length * width

# Access docstring
print(calculate_area.__doc__)
help(calculate_area)
```

---

## Parameters and Arguments

### Positional Parameters

```python
def introduce(name, age, city):
    print(f"{name} is {age} and lives in {city}")

introduce("Alice", 25, "NYC")
# Alice is 25 and lives in NYC
```

### Keyword Arguments

```python
def introduce(name, age, city):
    print(f"{name} is {age} and lives in {city}")

# Using keyword arguments (order doesn't matter)
introduce(city="NYC", name="Alice", age=25)
introduce(name="Bob", age=30, city="LA")
```

### Default Parameters

```python
def greet(name, greeting="Hello"):
    print(f"{greeting}, {name}!")

greet("Alice")                  # Hello, Alice!
greet("Bob", "Hi")              # Hi, Bob!
greet("Charlie", greeting="Hey") # Hey, Charlie!

# Mutable defaults (be careful!)
def add_to_list(item, my_list=None):  # ✅ Correct
    if my_list is None:
        my_list = []
    my_list.append(item)
    return my_list

# ❌ Don't do this
def add_to_list_bad(item, my_list=[]):
    my_list.append(item)
    return my_list
```

### Variable-Length Arguments

```python
# *args - Variable number of positional arguments
def sum_all(*args):
    total = 0
    for num in args:
        total += num
    return total

print(sum_all(1, 2, 3))        # 6
print(sum_all(1, 2, 3, 4, 5))  # 15

# **kwargs - Variable number of keyword arguments
def print_info(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")

print_info(name="Alice", age=25, city="NYC")
# name: Alice
# age: 25
# city: NYC

# Combining all types
def full_function(a, b, *args, **kwargs):
    print(f"a={a}, b={b}")
    print(f"args={args}")
    print(f"kwargs={kwargs}")

full_function(1, 2, 3, 4, name="Alice", age=25)
```

---

## Return Values

### Basic Return

```python
def add(a, b):
    return a + b

result = add(5, 3)
print(result)  # 8

# Early return
def check_age(age):
    if age < 0:
        return "Invalid age"
    if age < 18:
        return "Minor"
    return "Adult"

print(check_age(25))  # Adult
print(check_age(10))  # Minor
print(check_age(-5))  # Invalid age
```

### Multiple Return Values

```python
def get_coordinates():
    return 10, 20  # Returns tuple

x, y = get_coordinates()
print(x, y)  # 10 20

# Dictionary return
def get_user_info():
    return {
        "name": "Alice",
        "age": 25,
        "email": "alice@email.com"
    }

user = get_user_info()
print(user["name"])  # Alice

# List return
def process_data():
    return [1, 2, 3, 4, 5]

data = process_data()
print(data)  # [1, 2, 3, 4, 5]
```

---

## Scope

### Local Scope

```python
def my_function():
    x = 10  # Local variable
    print(x)

my_function()    # 10
# print(x)       # ❌ Error - x is not accessible here
```

### Global Scope

```python
x = 10  # Global variable

def my_function():
    print(x)  # Accessible

my_function()  # 10
print(x)       # 10

# Modifying global variable
counter = 0

def increment():
    global counter  # Tell Python to use global variable
    counter += 1

increment()
print(counter)  # 1
```

### Enclosing Scope (Closures)

```python
def outer():
    x = 10  # Enclosing scope
    
    def inner():
        print(x)  # Accessible from inner
    
    inner()

outer()  # 10

# Modifying enclosing variable
def outer():
    count = 0
    
    def increment():
        nonlocal count  # Modify enclosing variable
        count += 1
        return count
    
    print(increment())  # 1
    print(increment())  # 2

outer()
```

---

## Advanced Functions

### Lambda Functions

```python
# Anonymous functions
square = lambda x: x ** 2
print(square(5))  # 25

add = lambda x, y: x + y
print(add(3, 4))  # 7

# With map
numbers = [1, 2, 3, 4, 5]
doubled = list(map(lambda x: x * 2, numbers))
print(doubled)  # [2, 4, 6, 8, 10]

# With filter
numbers = [1, 2, 3, 4, 5, 6]
evens = list(filter(lambda x: x % 2 == 0, numbers))
print(evens)  # [2, 4, 6]
```

### Decorators (Introduction)

```python
def my_decorator(func):
    def wrapper():
        print("Something before function")
        func()
        print("Something after function")
    return wrapper

@my_decorator
def say_hello():
    print("Hello!")

say_hello()
# Output:
# Something before function
# Hello!
# Something after function
```

### Higher-Order Functions

```python
def apply_operation(x, y, operation):
    return operation(x, y)

def add(a, b):
    return a + b

def multiply(a, b):
    return a * b

print(apply_operation(5, 3, add))       # 8
print(apply_operation(5, 3, multiply))  # 15

# Returning functions
def multiplier(n):
    def multiply(x):
        return x * n
    return multiply

times_three = multiplier(3)
print(times_three(5))  # 15
print(times_three(10)) # 30
```

---

## Practical Examples

### Temperature Converter

```python
def celsius_to_fahrenheit(celsius):
    """Convert Celsius to Fahrenheit"""
    return (celsius * 9/5) + 32

def fahrenheit_to_celsius(fahrenheit):
    """Convert Fahrenheit to Celsius"""
    return (fahrenheit - 32) * 5/9

print(celsius_to_fahrenheit(0))      # 32.0
print(fahrenheit_to_celsius(212))    # 100.0
```

### Grade Calculator

```python
def calculate_grade(score):
    """Calculate grade from score"""
    if score >= 90:
        return "A"
    elif score >= 80:
        return "B"
    elif score >= 70:
        return "C"
    elif score >= 60:
        return "D"
    else:
        return "F"

def get_grade_description(grade):
    """Get description for grade"""
    grades = {
        "A": "Excellent",
        "B": "Good",
        "C": "Average",
        "D": "Poor",
        "F": "Fail"
    }
    return grades.get(grade, "Unknown")

score = 85
grade = calculate_grade(score)
description = get_grade_description(grade)
print(f"Score: {score}, Grade: {grade}, {description}")
# Score: 85, Grade: B, Good
```

### List Operations

```python
def find_max(numbers):
    """Find maximum number"""
    if not numbers:
        return None
    max_num = numbers[0]
    for num in numbers:
        if num > max_num:
            max_num = num
    return max_num

def find_min(numbers):
    """Find minimum number"""
    if not numbers:
        return None
    min_num = numbers[0]
    for num in numbers:
        if num < min_num:
            min_num = num
    return min_num

def calculate_average(numbers):
    """Calculate average of numbers"""
    if not numbers:
        return 0
    return sum(numbers) / len(numbers)

numbers = [10, 5, 20, 15, 8]
print(f"Max: {find_max(numbers)}")           # Max: 20
print(f"Min: {find_min(numbers)}")           # Min: 5
print(f"Average: {calculate_average(numbers):.2f}")  # Average: 11.60
```

### Data Validation

```python
def validate_email(email):
    """Validate email format"""
    return "@" in email and "." in email

def validate_password(password):
    """Validate password strength"""
    has_upper = any(c.isupper() for c in password)
    has_lower = any(c.islower() for c in password)
    has_digit = any(c.isdigit() for c in password)
    is_long_enough = len(password) >= 8
    
    return has_upper and has_lower and has_digit and is_long_enough

def validate_age(age):
    """Validate age"""
    try:
        age_int = int(age)
        return 0 < age_int < 150
    except ValueError:
        return False

print(validate_email("user@example.com"))        # True
print(validate_password("SecurePass123"))        # True
print(validate_age("25"))                        # True
```

---

## Best Practices

### 1. One Task Per Function
```python
# ❌ Bad - does too much
def process_user_data():
    # Reads file
    # Parses JSON
    # Validates data
    # Saves to database
    pass

# ✅ Good - single responsibility
def read_user_file():
    pass

def parse_user_json():
    pass

def validate_user_data():
    pass

def save_user_to_database():
    pass
```

### 2. Clear Naming
```python
# ❌ Bad
def f(x):
    return x * 2

# ✅ Good
def double_value(number):
    return number * 2
```

### 3. Use Type Hints
```python
def add_numbers(a: int, b: int) -> int:
    return a + b

def greet_user(name: str) -> str:
    return f"Hello, {name}!"
```

### 4. Limit Function Length
```python
# Keep functions short and focused
# If > 20 lines, consider breaking it up
```

---

## Summary

| Concept | Example |
|---------|---------|
| Basic function | `def func(): pass` |
| Parameters | `def func(a, b):` |
| Default params | `def func(a=1):` |
| Variable args | `def func(*args):` |
| Keyword args | `def func(**kwargs):` |
| Return value | `return x` |
| Lambda | `lambda x: x ** 2` |
| Global variable | `global x` |
| Nonlocal | `nonlocal x` |

---

**Next**: [Data Structures](../02-data-structures/)
