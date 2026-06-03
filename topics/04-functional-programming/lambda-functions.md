# Lambda Functions in Python: A Comprehensive Guide

## Table of Contents
1. [Introduction](#introduction)
2. [Syntax and Basics](#syntax-and-basics)
3. [Lambda vs Regular Functions](#lambda-vs-regular-functions)
4. [Common Use Cases](#common-use-cases)
5. [Advanced Techniques](#advanced-techniques)
6. [Best Practices](#best-practices)
7. [Summary](#summary)

## Introduction

Lambda functions are small anonymous functions defined with the `lambda` keyword. They're useful for short, simple operations where a full function definition would be overkill.

## Syntax and Basics

```python
# Basic lambda syntax: lambda arguments: expression

square = lambda x: x ** 2
print(square(5))  # Output: 25

add = lambda x, y: x + y
print(add(3, 4))  # Output: 7

# Multiple arguments
multiply = lambda x, y, z: x * y * z
print(multiply(2, 3, 4))  # Output: 24

# With default arguments
greet = lambda name="World": f"Hello, {name}!"
print(greet())        # Output: Hello, World!
print(greet("Alice"))  # Output: Hello, Alice!

# Conditional expressions
max_val = lambda x, y: x if x > y else y
print(max_val(10, 20))  # Output: 20
```

## Lambda vs Regular Functions

```python
# Lambda function
square_lambda = lambda x: x ** 2

# Equivalent regular function
def square_regular(x):
    return x ** 2

print(square_lambda(5))  # Output: 25
print(square_regular(5))  # Output: 25

# Lambda can't contain statements
# lambda x: if x > 0: print(x)  # SYNTAX ERROR

# Regular function can contain statements
def validate(x):
    if x > 0:
        print("Positive")
    else:
        print("Non-positive")
```

## Common Use Cases

### With map()
```python
numbers = [1, 2, 3, 4, 5]

# Square each number
squared = map(lambda x: x ** 2, numbers)
print(list(squared))  # Output: [1, 4, 9, 16, 25]

# Convert to strings
strings = map(lambda x: f"num_{x}", numbers)
print(list(strings))  # Output: ['num_1', 'num_2', 'num_3', 'num_4', 'num_5']
```

### With filter()
```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Filter even numbers
evens = filter(lambda x: x % 2 == 0, numbers)
print(list(evens))  # Output: [2, 4, 6, 8, 10]

# Filter numbers greater than 5
greater_than_5 = filter(lambda x: x > 5, numbers)
print(list(greater_than_5))  # Output: [6, 7, 8, 9, 10]
```

### With sorted()
```python
students = [
    {"name": "Alice", "grade": 85},
    {"name": "Bob", "grade": 92},
    {"name": "Charlie", "grade": 78}
]

# Sort by grade
by_grade = sorted(students, key=lambda s: s["grade"])
print(by_grade)
# Output: [{'name': 'Charlie', 'grade': 78}, {'name': 'Alice', 'grade': 85}, {'name': 'Bob', 'grade': 92}]

# Sort by name
by_name = sorted(students, key=lambda s: s["name"])
print(by_name)
# Output: [{'name': 'Alice', 'grade': 85}, {'name': 'Bob', 'grade': 92}, {'name': 'Charlie', 'grade': 78}]
```

### With reduce()
```python
from functools import reduce

numbers = [1, 2, 3, 4, 5]

# Sum all numbers
total = reduce(lambda x, y: x + y, numbers)
print(total)  # Output: 15

# Product
product = reduce(lambda x, y: x * y, numbers)
print(product)  # Output: 120

# Find maximum
maximum = reduce(lambda x, y: x if x > y else y, numbers)
print(maximum)  # Output: 5
```

## Advanced Techniques

### Lambda with Multiple Expressions (using tuple)
```python
# Can't use multiple statements, but can use tuple packing
operations = [
    ("add", lambda x, y: x + y),
    ("subtract", lambda x, y: x - y),
    ("multiply", lambda x, y: x * y)
]

def calculator(op_name, x, y):
    for name, op in operations:
        if name == op_name:
            return op(x, y)

print(calculator("add", 5, 3))       # Output: 8
print(calculator("multiply", 5, 3))  # Output: 15
```

### Lambda Closures
```python
def make_multiplier(n):
    return lambda x: x * n

times_2 = make_multiplier(2)
times_5 = make_multiplier(5)

print(times_2(10))  # Output: 20
print(times_5(10))  # Output: 50
```

## Best Practices

### 1. Keep Lambda Simple
```python
# GOOD - simple lambda
square = lambda x: x ** 2

# BAD - complex lambda
calculate = lambda x: (x ** 2) + (3 * x) - 2 if x > 0 else (x ** 2) - (3 * x) + 2

# BETTER - use regular function for complex logic
def calculate(x):
    base = x ** 2
    adjustment = 3 * x if x > 0 else -3 * x
    return base + adjustment - 2
```

### 2. Use Descriptive Names When Assigning
```python
# GOOD - clear what it does
get_item_price = lambda item: item["price"]

# BAD - unclear
f = lambda item: item["price"]
```

### 3. Prefer map/filter Over Loops for Functional Operations
```python
# GOOD - functional style
squared = list(map(lambda x: x ** 2, numbers))

# LESS GOOD - imperative style
squared = []
for x in numbers:
    squared.append(x ** 2)

# ALSO GOOD - list comprehension (more Pythonic)
squared = [x ** 2 for x in numbers]
```

### 4. Avoid Lambda in Default Arguments
```python
# PROBLEMATIC - default lambda called at definition time
def process_data(data, transform=lambda x: x):
    return [transform(item) for item in data]

# BETTER - use None as default
def process_data(data, transform=None):
    if transform is None:
        transform = lambda x: x
    return [transform(item) for item in data]
```

## Summary

| Use Case | Example |
|----------|---------|
| **Simple transformation** | `map(lambda x: x * 2, data)` |
| **Filtering** | `filter(lambda x: x > 0, data)` |
| **Sorting** | `sorted(data, key=lambda x: x["key"])` |
| **Reducing** | `reduce(lambda x, y: x + y, data)` |
| **Key function** | `dict.get("key", lambda: "default")` |

### Key Takeaways

1. **Lambda for short, simple functions** - not for complex logic
2. **Prefer list comprehensions over map/filter** - more readable in Python
3. **Use functools.reduce carefully** - explicit loops are often clearer
4. **Keep lambda expressions readable** - one-liners only
5. **Name lambda results descriptively** - improves code clarity
6. **Consider regular functions for complex operations** - more testable
7. **Use lambda in callbacks** - event handlers, sorting keys

### Practice Exercises

1. Sort a list of dictionaries by multiple fields using lambda
2. Transform data using map with lambda
3. Filter numbers based on multiple conditions
4. Create a function factory using lambda closures
5. Use reduce to calculate statistics

---

**Next:** Learn map, filter, and reduce for functional data processing!
