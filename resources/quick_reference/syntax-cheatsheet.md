# Quick Reference - Python Syntax Cheatsheet

Fast lookup guide for common Python syntax and operations.

## Basic Syntax

```python
# Comments
# Single line comment
""" Multi-line comment """

# Variables (dynamic typing)
name = "John"
age = 25
price = 19.99
is_valid = True

# Type conversion
int("123")      # String to int
str(123)        # Int to string
float("3.14")   # String to float
bool(1)         # Any to bool
```

## Data Types

```python
# Strings
text = "Hello"
text = 'World'
text = """Multi
line
string"""
text = f"Hello {name}"  # f-string

# Lists (mutable, ordered)
numbers = [1, 2, 3]
mixed = [1, "text", 3.14, True]
numbers.append(4)
numbers.extend([5, 6])
numbers.pop()
numbers.remove(2)

# Tuples (immutable, ordered)
coords = (10, 20)
a, b = coords  # Unpacking

# Dictionaries (key-value)
person = {"name": "John", "age": 25}
person["name"]
person.get("age", 0)
person.keys()
person.values()
person.items()

# Sets (unique, unordered)
unique = {1, 2, 3}
unique.add(4)
unique.remove(2)
```

## Control Flow

```python
# If statements
if age > 18:
    print("Adult")
elif age >= 13:
    print("Teen")
else:
    print("Child")

# Ternary operator
status = "Adult" if age > 18 else "Minor"

# Loops
for i in range(5):
    print(i)

for item in items:
    print(item)

while condition:
    # code
    if something:
        break
    if other:
        continue

# Loop with index
for i, item in enumerate(items):
    print(i, item)

# Loop over dictionary
for key, value in dict.items():
    print(key, value)
```

## Functions

```python
# Basic function
def greet(name):
    return f"Hello, {name}!"

# Default parameters
def greet(name="World"):
    return f"Hello, {name}!"

# Multiple parameters
def add(a, b):
    return a + b

# Variable arguments
def sum_all(*args):
    return sum(args)

# Keyword arguments
def print_info(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")

# Lambda (anonymous functions)
square = lambda x: x ** 2
result = map(lambda x: x * 2, [1, 2, 3])

# Docstrings
def function():
    """This is what the function does."""
    pass

help(function)
```

## String Operations

```python
text = "Hello World"

# Methods
text.lower()        # "hello world"
text.upper()        # "HELLO WORLD"
text.replace("World", "Python")
text.split()        # ["Hello", "World"]
" ".join(["a", "b", "c"])  # "a b c"

# Indexing (0-based)
text[0]             # "H"
text[-1]            # "d"
text[0:5]           # "Hello"
text[6:]            # "World"

# Checking
"World" in text     # True
text.startswith("Hello")
text.endswith("World")
len(text)           # 11

# Formatting
f"{name}: {age}"
"{}: {}".format(name, age)
"{1} {0}".format("World", "Hello")
```

## List Operations

```python
numbers = [1, 2, 3, 4, 5]

# Indexing
numbers[0]          # 1
numbers[-1]         # 5
numbers[1:3]        # [2, 3]

# Methods
numbers.append(6)
numbers.insert(0, 0)
numbers.remove(3)
numbers.pop()       # Remove last
numbers.pop(0)      # Remove first
numbers.index(3)    # Position of 3
numbers.count(1)    # Count of 1

# List comprehension
squares = [x**2 for x in numbers]
evens = [x for x in numbers if x % 2 == 0]

# Sorting
sorted_nums = sorted(numbers)
numbers.sort()      # In-place
numbers.reverse()
```

## Dictionary Operations

```python
person = {"name": "John", "age": 25, "city": "NYC"}

# Access
person["name"]
person.get("name")
person.get("email", "Not found")

# Modify
person["age"] = 26
person["email"] = "john@email.com"

# Delete
del person["city"]
person.pop("email")
person.clear()      # Remove all

# Iteration
for key in person:
    print(key)

for value in person.values():
    print(value)

for key, value in person.items():
    print(key, value)

# Dictionary comprehension
squares = {x: x**2 for x in range(5)}
```

## File Operations

```python
# Reading
with open("file.txt", "r") as f:
    content = f.read()      # Entire file
    lines = f.readlines()   # List of lines
    line = f.readline()     # Single line

# Writing
with open("file.txt", "w") as f:
    f.write("Hello")
    f.writelines(["line1\n", "line2\n"])

# Appending
with open("file.txt", "a") as f:
    f.write("New line\n")

# JSON
import json
json.dump(data, file)
json.load(file)
```

## Exception Handling

```python
try:
    # Code that might fail
    result = 10 / 0
except ZeroDivisionError:
    print("Cannot divide by zero")
except Exception as e:
    print(f"Error: {e}")
else:
    print("Success!")
finally:
    print("Cleanup")
```

## Imports

```python
import math
from math import sqrt
from math import sqrt as square_root
import math as m
from module import *
```

## Classes

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def greet(self):
        return f"Hello, I'm {self.name}"

# Creating instance
person = Person("John", 25)
print(person.greet())

# Inheritance
class Employee(Person):
    def __init__(self, name, age, job):
        super().__init__(name, age)
        self.job = job
```

## Common Built-in Functions

```python
len(obj)            # Length
type(obj)           # Type
isinstance(obj, str)  # Check type
str(), int(), float()  # Convert
abs(-5)             # Absolute
round(3.7)          # Round
min(1, 2, 3)        # Minimum
max(1, 2, 3)        # Maximum
sum([1, 2, 3])      # Sum
all([True, True])   # All true?
any([False, True])  # Any true?
sorted([3, 1, 2])   # Sort
reversed([1, 2, 3])  # Reverse
enumerate([a, b])   # Index + item
zip([1, 2], [a, b])  # Combine lists
```

## Operators

```python
# Arithmetic
+, -, *, /, //, %, **

# Comparison
==, !=, <, >, <=, >=

# Logical
and, or, not

# Membership
in, not in

# Identity
is, is not
```

---

**Pro Tip**: Use `help()` function in Python REPL for quick documentation
