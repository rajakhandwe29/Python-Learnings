# Dictionaries in Python: A Comprehensive Guide

## Table of Contents
1. [Introduction](#introduction)
2. [Creating Dictionaries](#creating-dictionaries)
3. [Accessing and Modifying](#accessing-and-modifying)
4. [Dictionary Methods](#dictionary-methods)
5. [Iteration](#iteration)
6. [Dictionary Comprehensions](#dictionary-comprehensions)
7. [Nested Dictionaries](#nested-dictionaries)
8. [Advanced Patterns](#advanced-patterns)
9. [Practical Applications](#practical-applications)
10. [Common Mistakes](#common-mistakes)
11. [Best Practices](#best-practices)
12. [Performance Optimization](#performance-optimization)
13. [Summary](#summary)

## Introduction

Dictionaries are one of Python's most powerful and versatile data structures. A dictionary is an unordered (in Python < 3.7) or insertion-ordered (Python 3.7+) collection of key-value pairs. Unlike lists that use integer indices, dictionaries use keys—which can be any immutable type—to access values.

### Why Dictionaries Matter

Dictionaries are fundamental to Python programming because they:
- Map unique keys to values (fast O(1) lookup)
- Enable flexible data structure representation
- Power function keyword arguments
- Form the basis of JSON-like data handling
- Are used internally by Python for variable namespaces

### Quick Example

```python
# Creating a simple dictionary
user = {
    "name": "Alice",
    "age": 30,
    "email": "alice@example.com"
}

# Accessing values
print(user["name"])  # Output: Alice
print(user["age"])   # Output: 30

# Modifying values
user["age"] = 31
user["city"] = "New York"

print(user)
# Output: {'name': 'Alice', 'age': 31, 'email': 'alice@example.com', 'city': 'New York'}
```

## Creating Dictionaries

### Literal Syntax

```python
# Empty dictionary
empty = {}

# Dictionary with initial values
person = {
    "name": "Bob",
    "age": 28,
    "city": "Boston"
}

# Mixed key and value types
mixed = {
    1: "one",
    "two": 2,
    3.0: [1, 2, 3],
    True: "boolean key"
}

# Keys must be immutable types
valid_dict = {
    (1, 2): "tuple key",
    "string": "string key",
    42: "int key"
}

# Lists CANNOT be keys (mutable)
# invalid = {[1, 2]: "value"}  # TypeError
```

### Using dict() Constructor

```python
# From key-value pairs
d1 = dict(name="Charlie", age=35, city="Chicago")
print(d1)
# Output: {'name': 'Charlie', 'age': 35, 'city': 'Chicago'}

# From a sequence of pairs
d2 = dict([("x", 10), ("y", 20), ("z", 30)])
print(d2)
# Output: {'x': 10, 'y': 20, 'z': 30}

# From another dictionary (creates a copy)
original = {"a": 1, "b": 2}
copy = dict(original)
print(copy)
# Output: {'a': 1, 'b': 2}

# From keys with default value
keys = ["red", "green", "blue"]
d3 = dict.fromkeys(keys, 0)
print(d3)
# Output: {'red': 0, 'green': 0, 'blue': 0}
```

## Accessing and Modifying

### Accessing Values

```python
student = {
    "name": "Diana",
    "grade": "A",
    "subjects": ["Math", "Science"]
}

# Using bracket notation
print(student["name"])  # Output: Diana

# Using .get() with default value
print(student.get("name"))           # Output: Diana
print(student.get("age"))            # Output: None
print(student.get("age", "Unknown")) # Output: Unknown

# Check if key exists
if "grade" in student:
    print(f"Grade: {student['grade']}")

# Get with error handling
try:
    print(student["age"])
except KeyError:
    print("Age not found in dictionary")
```

### Modifying Values

```python
config = {
    "host": "localhost",
    "port": 8000,
    "debug": True
}

# Update existing key
config["port"] = 3000
print(config["port"])  # Output: 3000

# Add new key
config["database"] = "postgresql"
print(config)
# Output: {'host': 'localhost', 'port': 3000, 'debug': True, 'database': 'postgresql'}

# Update with .update()
config.update({"debug": False, "workers": 4})
print(config)
# Output: {'host': 'localhost', 'port': 3000, 'debug': False, 'database': 'postgresql', 'workers': 4}

# Update only if key doesn't exist
config.setdefault("timeout", 30)
print(config.get("timeout"))  # Output: 30

config.setdefault("timeout", 60)  # Won't change existing value
print(config.get("timeout"))  # Output: 30
```

### Deleting Values

```python
inventory = {
    "apples": 5,
    "bananas": 3,
    "oranges": 7
}

# Remove and return value
removed = inventory.pop("bananas")
print(removed)  # Output: 3
print(inventory)
# Output: {'apples': 5, 'oranges': 7}

# Pop with default value
removed = inventory.pop("grapes", "Not in stock")
print(removed)  # Output: Not in stock

# Remove all items
inventory.clear()
print(inventory)  # Output: {}

# Delete specific key
data = {"a": 1, "b": 2, "c": 3}
del data["b"]
print(data)  # Output: {'a': 1, 'c': 3}

# Delete dictionary itself
del data
# print(data)  # NameError: name 'data' is not defined
```

## Dictionary Methods

### Key, Value, and Item Views

```python
user_data = {
    "username": "john_doe",
    "email": "john@example.com",
    "verified": True
}

# Get all keys
keys = user_data.keys()
print(keys)  # Output: dict_keys(['username', 'email', 'verified'])
print(list(keys))  # Output: ['username', 'email', 'verified']

# Get all values
values = user_data.values()
print(values)
# Output: dict_values(['john_doe', 'john@example.com', True])

# Get all key-value pairs
items = user_data.items()
print(items)
# Output: dict_items([('username', 'john_doe'), ('email', 'john@example.com'), ('verified', True)])

# These are view objects (dynamic)
print("username" in user_data.keys())  # Output: True
```

### Copying Dictionaries

```python
original = {
    "name": "Eve",
    "scores": [85, 90, 92]
}

# Shallow copy (default)
shallow = original.copy()
shallow["name"] = "Frank"
shallow["scores"].append(95)

print(original["name"])      # Output: Eve
print(original["scores"])    # Output: [85, 90, 92, 95] - CHANGED!

# The list inside was shared (shallow copy)

# Deep copy (for nested structures)
import copy
original = {
    "name": "Grace",
    "scores": [85, 90, 92]
}

deep = copy.deepcopy(original)
deep["name"] = "Henry"
deep["scores"].append(95)

print(original["name"])      # Output: Grace
print(original["scores"])    # Output: [85, 90, 92] - NOT CHANGED
```

## Iteration

### Iterating Over Keys

```python
languages = {"Python": 1991, "Java": 1995, "Go": 2009}

# Implicit iteration over keys
for lang in languages:
    print(lang)
# Output: Python, Java, Go

# Explicit iteration over keys
for lang in languages.keys():
    print(f"{lang}: {languages[lang]}")
# Output: Python: 1991, Java: 1995, Go: 2009
```

### Iterating Over Values

```python
temperatures = {"Monday": 72, "Tuesday": 75, "Wednesday": 70}

for temp in temperatures.values():
    print(f"Temperature: {temp}°F")
# Output: Temperature: 72°F, Temperature: 75°F, Temperature: 70°F

# Calculate average temperature
avg = sum(temperatures.values()) / len(temperatures)
print(f"Average: {avg:.1f}°F")  # Output: Average: 72.3°F
```

### Iterating Over Items

```python
students = {
    "Alice": 95,
    "Bob": 87,
    "Charlie": 92
}

# Iterate with tuple unpacking
for name, score in students.items():
    grade = "A" if score >= 90 else "B" if score >= 80 else "C"
    print(f"{name}: {score} ({grade})")
# Output:
# Alice: 95 (A)
# Bob: 87 (B)
# Charlie: 92 (A)
```

### Sorted Iteration

```python
scores = {"Charlie": 88, "Alice": 95, "Bob": 82}

# Sort by key
print("Sorted by name:")
for name, score in sorted(scores.items()):
    print(f"{name}: {score}")
# Output: Alice: 95, Bob: 82, Charlie: 88

# Sort by value
print("\nSorted by score:")
for name, score in sorted(scores.items(), key=lambda x: x[1], reverse=True):
    print(f"{name}: {score}")
# Output: Alice: 95, Charlie: 88, Bob: 82
```

## Dictionary Comprehensions

### Basic Syntax

```python
# Create dictionary from list
squares = {x: x**2 for x in range(5)}
print(squares)
# Output: {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}

# Create dictionary from another dictionary
original = {"a": 1, "b": 2, "c": 3}
doubled = {k: v*2 for k, v in original.items()}
print(doubled)
# Output: {'a': 2, 'b': 4, 'c': 6}

# With condition
even_squares = {x: x**2 for x in range(10) if x % 2 == 0}
print(even_squares)
# Output: {0: 0, 2: 4, 4: 16, 6: 36, 8: 64}
```

### Advanced Comprehensions

```python
# Swap keys and values
word_to_letter = {"one": "a", "two": "b", "three": "c"}
letter_to_word = {v: k for k, v in word_to_letter.items()}
print(letter_to_word)
# Output: {'a': 'one', 'b': 'two', 'c': 'three'}

# Group by condition
numbers = range(1, 11)
grouped = {
    "even": [n for n in numbers if n % 2 == 0],
    "odd": [n for n in numbers if n % 2 != 0]
}
print(grouped)
# Output: {'even': [2, 4, 6, 8, 10], 'odd': [1, 3, 5, 7, 9]}

# Flatten nested structure
matrix = [[1, 2], [3, 4], [5, 6]]
flattened = {f"pos_{i}_{j}": val for i, row in enumerate(matrix) for j, val in enumerate(row)}
print(flattened)
# Output: {'pos_0_0': 1, 'pos_0_1': 2, 'pos_1_0': 3, 'pos_1_1': 4, 'pos_2_0': 5, 'pos_2_1': 6}
```

## Nested Dictionaries

### Creating Nested Structures

```python
# Company organization structure
company = {
    "name": "TechCorp",
    "departments": {
        "engineering": {
            "head": "Alice",
            "employees": 15,
            "budget": 500000
        },
        "marketing": {
            "head": "Bob",
            "employees": 5,
            "budget": 100000
        }
    }
}

# Accessing nested values
print(company["departments"]["engineering"]["head"])  # Output: Alice
print(company["departments"]["marketing"]["budget"])  # Output: 100000
```

### Working with Nested Dictionaries

```python
# Safe access with .get()
company_data = {
    "sales": {
        "q1": 50000,
        "q2": 65000
    }
}

# Accessing nested with multiple .get()
q1_sales = company_data.get("sales", {}).get("q1", 0)
print(q1_sales)  # Output: 50000

# Using defaultdict for automatic nested creation
from collections import defaultdict

# This prevents KeyError for nested access
nested = defaultdict(dict)
nested["user"]["name"] = "Charlie"
nested["user"]["email"] = "charlie@example.com"

print(dict(nested))
# Output: {'user': {'name': 'Charlie', 'email': 'charlie@example.com'}}
```

### Iterating Through Nested Dictionaries

```python
# Recursive iteration
inventory = {
    "warehouse_a": {
        "electronics": 45,
        "furniture": 12
    },
    "warehouse_b": {
        "electronics": 78,
        "furniture": 23
    }
}

def print_inventory(inv, indent=0):
    for location, items in inv.items():
        print("  " * indent + f"{location}:")
        if isinstance(items, dict):
            print_inventory(items, indent + 1)
        else:
            print("  " * (indent + 1) + f"Count: {items}")

print_inventory(inventory)
# Output:
# warehouse_a:
#   electronics:
#     Count: 45
#   furniture:
#     Count: 12
# warehouse_b:
#   electronics:
#     Count: 78
#   furniture:
#     Count: 23
```

## Advanced Patterns

### Counter for Frequency Tracking

```python
from collections import Counter

# Count frequency of elements
text = "hello world"
char_count = Counter(text)
print(char_count)
# Output: Counter({'l': 3, 'o': 2, 'h': 1, 'e': 1, ' ': 1, 'w': 1, 'r': 1, 'd': 1})

# Most common elements
print(char_count.most_common(3))
# Output: [('l', 3), ('o', 2), ('h', 1)]

# Word frequency
words = ["apple", "banana", "apple", "cherry", "banana", "apple"]
word_freq = Counter(words)
print(word_freq)
# Output: Counter({'apple': 3, 'banana': 2, 'cherry': 1})
```

### DefaultDict for Default Values

```python
from collections import defaultdict

# Regular dict raises KeyError for missing keys
regular = {}
# print(regular["missing"])  # KeyError

# defaultdict provides default value
default_dict = defaultdict(list)
default_dict["colors"].append("red")
default_dict["colors"].append("blue")

print(dict(default_dict))
# Output: {'colors': ['red', 'blue']}

# Different default types
int_dict = defaultdict(int)
int_dict["count"] += 1  # Starts at 0, then increments
print(dict(int_dict))
# Output: {'count': 1}

# Custom default factory
default_dict = defaultdict(lambda: {"active": True, "value": 0})
default_dict["user1"]["value"] = 100
print(dict(default_dict))
# Output: {'user1': {'active': True, 'value': 100}}
```

### OrderedDict for Insertion Order (Python < 3.7)

```python
from collections import OrderedDict

# In Python 3.7+, regular dicts maintain insertion order
# But OrderedDict provides additional methods

ordered = OrderedDict([("z", 26), ("a", 1), ("m", 13)])
print(ordered)
# Output: OrderedDict([('z', 26), ('a', 1), ('m', 13)])

# Move to end
ordered.move_to_end("a")
print(ordered)
# Output: OrderedDict([('z', 26), ('m', 13), ('a', 1)])

# Last item
print(ordered.popitem())
# Output: ('a', 1)
```

## Practical Applications

### Configuration Management

```python
# Application settings
config = {
    "database": {
        "host": "localhost",
        "port": 5432,
        "name": "myapp",
        "credentials": {
            "user": "admin",
            "password": "secret123"
        }
    },
    "server": {
        "host": "0.0.0.0",
        "port": 8000,
        "workers": 4
    }
}

def get_config_value(config, *keys, default=None):
    """Safely navigate nested config"""
    for key in keys:
        if isinstance(config, dict):
            config = config.get(key, {})
        else:
            return default
    return config if config != {} else default

db_user = get_config_value(config, "database", "credentials", "user")
print(f"Database user: {db_user}")  # Output: Database user: admin
```

### Caching Results

```python
# Simple memoization with dictionary
def fibonacci(n, cache={}):
    """Calculate fibonacci with caching"""
    if n in cache:
        return cache[n]
    
    if n <= 1:
        result = n
    else:
        result = fibonacci(n-1, cache) + fibonacci(n-2, cache)
    
    cache[n] = result
    return result

print(fibonacci(10))  # Output: 55
print(fibonacci.cache)  # Show cached values

# Better: use functools.lru_cache
from functools import lru_cache

@lru_cache(maxsize=128)
def fib(n):
    if n <= 1:
        return n
    return fib(n-1) + fib(n-2)

print(fib(35))  # Computes quickly with caching
print(fib.cache_info())  # See cache statistics
```

### Data Aggregation

```python
# Group data by category
sales_data = [
    {"date": "2024-01-01", "region": "North", "amount": 1000},
    {"date": "2024-01-02", "region": "South", "amount": 1500},
    {"date": "2024-01-01", "region": "South", "amount": 1200},
    {"date": "2024-01-02", "region": "North", "amount": 1300},
]

# Group by region and aggregate
from collections import defaultdict

regional_sales = defaultdict(list)
for sale in sales_data:
    regional_sales[sale["region"]].append(sale["amount"])

# Calculate totals by region
regional_totals = {region: sum(amounts) for region, amounts in regional_sales.items()}
print(regional_totals)
# Output: {'North': 2300, 'South': 2700}
```

### JSON-like Data Processing

```python
import json

# Working with JSON data (common in web APIs)
json_data = '''
{
    "users": [
        {"id": 1, "name": "Alice", "age": 30},
        {"id": 2, "name": "Bob", "age": 25}
    ],
    "total": 2
}
'''

data = json.loads(json_data)

# Access nested data
for user in data["users"]:
    print(f"{user['name']}: {user['age']} years old")

# Convert back to JSON
output = json.dumps(data, indent=2)
print(output)
```

## Common Mistakes

### Mistake 1: Using Mutable Keys

```python
# WRONG - lists cannot be dictionary keys
try:
    d = {[1, 2]: "value"}
except TypeError:
    print("Lists cannot be dictionary keys")

# CORRECT - use tuples instead
d = {(1, 2): "value"}
print(d[(1, 2)])  # Output: value
```

### Mistake 2: KeyError from Direct Access

```python
# WRONG - raises KeyError if key missing
user = {"name": "Alice"}
# print(user["email"])  # KeyError: 'email'

# CORRECT - use .get() with default
print(user.get("email", "Not provided"))  # Output: Not provided

# CORRECT - check if key exists first
if "email" in user:
    print(user["email"])
```

### Mistake 3: Modifying Dictionary While Iterating

```python
# WRONG - can cause skipped items or errors
d = {"a": 1, "b": 2, "c": 3}
# for key in d:
#     if key == "b":
#         del d[key]  # RuntimeError!

# CORRECT - iterate over a copy of keys
d = {"a": 1, "b": 2, "c": 3}
for key in list(d.keys()):
    if key == "b":
        del d[key]
print(d)  # Output: {'a': 1, 'c': 3}
```

### Mistake 4: Shallow Copy Issues

```python
# WRONG - modifying nested structure
original = {"data": [1, 2, 3]}
copy = original.copy()
copy["data"].append(4)
print(original)  # Output: {'data': [1, 2, 3, 4]} - MODIFIED!

# CORRECT - use deepcopy for nested structures
import copy
original = {"data": [1, 2, 3]}
deep_copy = copy.deepcopy(original)
deep_copy["data"].append(4)
print(original)  # Output: {'data': [1, 2, 3]} - NOT MODIFIED
```

### Mistake 5: Case Sensitivity Issues

```python
# WRONG - keys are case-sensitive
config = {"Debug": True}
# print(config["debug"])  # KeyError: 'debug'

# CORRECT - handle case properly
config = {"debug": True}
print(config.get("debug"))  # Output: True

# Or normalize case
user_input = "DEBUG"
config = {"debug": True}
if user_input.lower() in config:
    print(config[user_input.lower()])
```

## Best Practices

### 1. Use .get() for Safe Access

```python
# Good - safe access with default value
user = {"name": "Charlie"}
print(user.get("name", "Unknown"))       # Output: Charlie
print(user.get("email", "Not provided")) # Output: Not provided

# Good - with more complex defaults
config = {}
timeout = config.get("timeout", 30)
print(timeout)  # Output: 30
```

### 2. Use Dictionary Comprehensions

```python
# Good - concise and readable
numbers = [1, 2, 3, 4, 5]
squares = {n: n**2 for n in numbers}
print(squares)  # Output: {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

# Good - with filtering
even_squares = {n: n**2 for n in numbers if n % 2 == 0}
print(even_squares)  # Output: {2: 4, 4: 16}
```

### 3. Use Meaningful Key Names

```python
# Bad - unclear abbreviations
user = {"nm": "Alice", "ag": 30, "em": "alice@example.com"}

# Good - descriptive keys
user = {"name": "Alice", "age": 30, "email": "alice@example.com"}

# Good - nested for related data
user = {
    "name": "Alice",
    "contact": {
        "email": "alice@example.com",
        "phone": "555-1234"
    },
    "profile": {
        "age": 30,
        "location": "NYC"
    }
}
```

### 4. Handle Missing Data Gracefully

```python
# Good - explicit error handling
def safe_get_nested(data, *keys, default=None):
    """Safely get nested dictionary value"""
    for key in keys:
        if isinstance(data, dict):
            data = data.get(key)
            if data is None:
                return default
        else:
            return default
    return data

nested = {"user": {"profile": {"age": 30}}}
age = safe_get_nested(nested, "user", "profile", "age")
print(age)  # Output: 30

missing = safe_get_nested(nested, "user", "settings", "theme", default="light")
print(missing)  # Output: light
```

## Performance Optimization

### Lookup Performance

```python
import timeit

# Dictionary lookup is O(1) on average
d = {i: i**2 for i in range(1000)}

dict_lookup = timeit.timeit(lambda: 500 in d, number=1000000)
print(f"Dictionary lookup: {dict_lookup:.6f}s")

# Compare to list lookup O(n)
lst = list(range(1000))
list_lookup = timeit.timeit(lambda: 500 in lst, number=1000000)
print(f"List lookup: {list_lookup:.6f}s")

# Dictionary is significantly faster for large collections
```

### Memory Efficient Storage

```python
import sys

# Dictionary memory usage
d = {i: str(i) for i in range(100)}
print(f"Dictionary size: {sys.getsizeof(d)} bytes")

# vs Lists
lst = [(i, str(i)) for i in range(100)]
print(f"List size: {sys.getsizeof(lst)} bytes")

# Dictionaries use more memory but provide O(1) access
# Lists use less memory but have O(n) access time
```

## Summary

| Feature | Details |
|---------|---------|
| **Definition** | Unordered (Python < 3.7) or ordered collection of key-value pairs |
| **Creation** | `{}`, `{"key": "value"}`, `dict()`, dict comprehensions |
| **Access** | `dict[key]` or `dict.get(key, default)` |
| **Modification** | `dict[key] = value`, `.update()`, `.setdefault()` |
| **Keys** | Must be immutable (strings, numbers, tuples) |
| **Values** | Can be any type (lists, dicts, etc.) |
| **Iteration** | `.keys()`, `.values()`, `.items()` |
| **Lookup Time** | O(1) average case, O(n) worst case |
| **Memory** | More than lists, but provides fast access |
| **Hashable** | Dictionaries themselves are not hashable |
| **Nesting** | Can contain other dictionaries |
| **Common Methods** | `.get()`, `.pop()`, `.update()`, `.clear()`, `.copy()` |

### Key Takeaways

1. **Use dictionaries for key-value mappings** - much faster than searching lists
2. **Always use .get() for safe access** - avoids KeyError exceptions
3. **Dictionary keys must be immutable** - use tuples instead of lists
4. **Use dictionaries for configuration** - flexible and readable
5. **Dictionary comprehensions are powerful** - use them for creating dictionaries
6. **Deep copy nested dictionaries** - shallow copy can cause unintended modifications
7. **Collections module provides alternatives** - defaultdict, Counter, OrderedDict

### Practice Exercises

1. Create a phone book dictionary and implement search, add, update, and delete functions
2. Write a function that finds the most common words in a text using Counter
3. Implement a simple cache using defaultdict with callable default factory
4. Create a nested dictionary representing a school with departments and students
5. Build a word frequency analyzer that returns top 10 most common words

---

**Next:** Explore sets for unique collections, or continue with other data structures for comprehensive Python mastery.
