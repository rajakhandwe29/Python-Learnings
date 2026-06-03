# Variables and Data Types

Understanding how Python handles data storage and type systems.

## Table of Contents
1. [Variables](#variables)
2. [Data Types](#data-types)
3. [Type Conversion](#type-conversion)
4. [Type Checking](#type-checking)
5. [Best Practices](#best-practices)

---

## Variables

### What is a Variable?

A variable is a named location in memory that stores a value. Think of it like a labeled box where you can put something inside. Unlike some programming languages (like Java or C++), Python variables don't require you to declare their type upfront - Python is smart enough to figure out what type of data you're storing based on what you assign to it. This is called "dynamic typing."

**Why variables matter**: Variables let you store data and reuse it throughout your program. Without variables, you'd have to type the same values over and over, which would be inefficient and error-prone.

**How it works**: When you write `name = "John"`, Python:
1. Creates a box in memory
2. Labels it "name"
3. Puts "John" inside
4. Now whenever you use `name`, Python knows to look inside that box

Here's the practical example:

```python
# Creating variables - Python automatically determines the type
name = "John"           # String (text data)
age = 25               # Integer (whole number)
height = 5.9           # Float (decimal number)
is_student = True      # Boolean (True/False)

# Using variables - print them out
print(name, age, height, is_student)
# Output: John 25 5.9 True

# You can also print them individually
print(f"Name: {name}")          # Name: John
print(f"Age: {age}")            # Age: 25
print(f"Height: {height}m")     # Height: 5.9m
print(f"Student: {is_student}") # Student: True
```

**Key insight**: Notice how we didn't write anything like "String name = John" or "int age = 25". Python figures it out automatically. This makes Python easier to write but also means you need to be careful about what data you put in each variable.

### Variable Naming Conventions

```python
# ✅ Good naming
user_name = "Alice"
total_amount = 100
is_active = True
MAX_ATTEMPTS = 5

# ❌ Bad naming
a = "Alice"           # Too vague
userName = "Alice"    # Should use snake_case
total_amount_$$ = 100 # Invalid characters
2users = []           # Can't start with number
```

### Naming Rules

1. **Must start** with letter (a-z, A-Z) or underscore (_)
2. **Can contain** letters, numbers, underscores
3. **Case sensitive** - `age` ≠ `Age`
4. **Avoid keywords** - don't use `if`, `for`, `while`, etc.
5. **Use snake_case** - for standard variables
6. **Use UPPER_CASE** - for constants

```python
import keyword
print(keyword.kwlist)  # All reserved keywords
```

### Multiple Assignment

```python
# Multiple assignments
x = y = z = 0  # All set to 0

# Unpacking
a, b, c = 1, 2, 3
print(a, b, c)  # 1 2 3

# Swapping
x, y = 1, 2
x, y = y, x  # x=2, y=1

# From lists/tuples
values = [10, 20, 30]
a, b, c = values
```

---

## Data Types

Python has several built-in data types:

### 1. Integers (int)

Whole numbers, positive or negative, without decimal points.

```python
# Creating integers
count = 10
temperature = -5
big_number = 1_000_000  # Underscores for readability

# Type checking
print(type(count))  # <class 'int'>

# Integer operations
print(10 + 5)        # 15 (addition)
print(10 - 3)        # 7 (subtraction)
print(10 * 2)        # 20 (multiplication)
print(10 // 3)       # 3 (floor division)
print(10 % 3)        # 1 (modulo)
print(10 ** 2)       # 100 (exponentiation)

# Large numbers (unlimited precision)
large = 99999999999999999999999999999
print(large + 1)  # No overflow!
```

### 2. Floats (float)

Numbers with decimal points.

```python
# Creating floats
price = 19.99
temperature = -3.14
scientific = 1.5e-3  # 0.0015

# Type checking
print(type(price))  # <class 'float'>

# Float operations
print(10.5 + 2.3)    # 12.8
print(10.5 - 2.3)    # 8.2
print(10.5 * 2)      # 21.0
print(10.5 / 3)      # 3.5

# Floating point precision
print(0.1 + 0.2)     # 0.30000000000000004 (precision issue!)

# Solution: Use Decimal
from decimal import Decimal
print(Decimal('0.1') + Decimal('0.2'))  # 0.3
```

### 3. Strings (str)

Text data enclosed in quotes.

```python
# Creating strings
single = 'Hello'
double = "World"
multi = """This is
a multi-line
string"""

# f-strings (formatted strings) - PREFERRED
name = "Alice"
age = 25
message = f"My name is {name} and I'm {age} years old"
print(message)  # My name is Alice and I'm 25 years old

# String concatenation
greeting = "Hello" + " " + "World"
print(greeting)  # Hello World

# String repetition
print("Ha" * 3)  # HaHaHa

# Accessing characters
text = "Python"
print(text[0])    # P (first character)
print(text[-1])   # n (last character)
print(text[1:4])  # yth (slice)

# String methods
text = "hello world"
print(text.upper())           # HELLO WORLD
print(text.capitalize())      # Hello world
print(text.title())           # Hello World
print(text.replace("o", "0")) # hell0 w0rld
print(text.split())           # ['hello', 'world']

# String length
print(len("Python"))  # 6
```

### 4. Booleans (bool)

True or False values.

```python
# Creating booleans
is_active = True
is_admin = False

print(type(is_active))  # <class 'bool'>

# Boolean operations
print(True and False)   # False
print(True or False)    # True
print(not True)         # False

# Comparing values
print(10 > 5)          # True
print(10 == 5)         # False
print(10 != 5)         # True

# Truthy and Falsy values
print(bool(0))         # False (falsy)
print(bool(1))         # True (truthy)
print(bool(""))        # False (empty string is falsy)
print(bool("text"))    # True (non-empty string is truthy)
print(bool([]))        # False (empty list is falsy)
print(bool([1, 2]))    # True (non-empty list is truthy)
```

### 5. Lists (list)

Ordered, mutable collection of items.

```python
# Creating lists
empty_list = []
numbers = [1, 2, 3, 4, 5]
mixed = [1, "text", 3.14, True]

# Accessing elements
print(numbers[0])      # 1
print(numbers[-1])     # 5
print(numbers[1:3])    # [2, 3]

# Modifying lists
numbers.append(6)           # Add to end
numbers.insert(0, 0)        # Insert at position
numbers.extend([7, 8])      # Add multiple items
numbers.remove(1)           # Remove first occurrence
popped = numbers.pop()      # Remove and return last item
numbers[0] = 10             # Change element

# List methods
my_list = [3, 1, 4, 1, 5]
print(my_list.count(1))     # 2
print(my_list.index(4))     # 2
my_list.sort()              # Sort in place
my_list.reverse()           # Reverse in place

# List comprehension
squares = [x**2 for x in range(5)]  # [0, 1, 4, 9, 16]
evens = [x for x in range(10) if x % 2 == 0]  # [0, 2, 4, 6, 8]
```

### 6. Tuples (tuple)

Ordered, immutable collection of items.

```python
# Creating tuples
empty_tuple = ()
single_item = (1,)           # Note the comma!
coordinates = (10, 20)
mixed = (1, "text", 3.14)

# Accessing elements
print(coordinates[0])  # 10
print(coordinates[-1]) # 20

# Immutability
coordinates = (10, 20)
# coordinates[0] = 5   # ❌ Error! Can't modify

# Tuple unpacking
x, y = (10, 20)
print(x, y)  # 10 20

# Tuple operations
tuple1 = (1, 2)
tuple2 = (3, 4)
combined = tuple1 + tuple2  # (1, 2, 3, 4)
repeated = (1, 2) * 3      # (1, 2, 1, 2, 1, 2)

# Using tuples as dictionary keys (immutable!)
coordinates = {(0, 0): "origin", (1, 1): "diagonal"}
print(coordinates[(0, 0)])  # origin
```

### 7. Dictionaries (dict)

Unordered (ordered in Python 3.7+), mutable key-value pairs.

```python
# Creating dictionaries
empty_dict = {}
person = {"name": "Alice", "age": 25, "city": "NYC"}

# Accessing values
print(person["name"])           # Alice
print(person.get("age"))        # 25
print(person.get("job", "N/A")) # N/A (default value)

# Adding/Updating items
person["job"] = "Engineer"
person.update({"email": "alice@email.com"})

# Removing items
del person["city"]
person.pop("job")

# Dictionary methods
print(person.keys())    # dict_keys(['name', 'age', ...])
print(person.values())  # dict_values(['Alice', 25, ...])
print(person.items())   # dict_items([('name', 'Alice'), ...])

# Iterating
for key, value in person.items():
    print(f"{key}: {value}")

# Dictionary comprehension
squares = {x: x**2 for x in range(5)}  # {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

### 8. Sets (set)

Unordered, mutable collection of unique items.

```python
# Creating sets
empty_set = set()  # Note: {} creates dict, not set
numbers = {1, 2, 3, 4, 5}
mixed = {1, "text", 3.14}

# Adding items
numbers.add(6)
numbers.update([7, 8, 9])

# Removing items
numbers.remove(1)  # Raises error if not found
numbers.discard(2) # Doesn't raise error if not found

# Set operations
set1 = {1, 2, 3}
set2 = {2, 3, 4}

print(set1 | set2)    # Union: {1, 2, 3, 4}
print(set1 & set2)    # Intersection: {2, 3}
print(set1 - set2)    # Difference: {1}
print(set1 ^ set2)    # Symmetric difference: {1, 4}

# Set methods
print(set1.issubset(set2))      # False
print(set1.issuperset(set2))    # False
print(set1.isdisjoint(set2))    # False (have common elements)

# Removing duplicates
numbers = [1, 2, 2, 3, 3, 3, 4]
unique = set(numbers)           # {1, 2, 3, 4}
unique_list = list(unique)      # [1, 2, 3, 4]
```

---

## Type Conversion

Converting between different data types.

```python
# String to Integer
age_str = "25"
age = int(age_str)  # 25

# String to Float
price_str = "19.99"
price = float(price_str)  # 19.99

# Integer to String
count = 100
count_str = str(count)  # "100"

# Float to Integer (truncates decimal)
value = 3.9
integer_value = int(value)  # 3

# String to Boolean
bool("True")      # True
bool("")          # False (empty string is falsy)

# List to Tuple
numbers = [1, 2, 3]
tuple_nums = tuple(numbers)  # (1, 2, 3)

# Tuple to List
coords = (10, 20)
list_coords = list(coords)   # [10, 20]

# Any to String representation
print(str(123))      # "123"
print(str(True))     # "True"
print(str([1, 2]))   # "[1, 2]"
```

---

## Type Checking

Determining the type of a variable.

```python
# Using type()
print(type(10))              # <class 'int'>
print(type(3.14))            # <class 'float'>
print(type("hello"))         # <class 'str'>
print(type(True))            # <class 'bool'>
print(type([1, 2]))          # <class 'list'>

# Using isinstance()
value = 10
print(isinstance(value, int))        # True
print(isinstance(value, (int, float)))  # Check multiple types

# Type annotations (hints - don't enforce)
def greet(name: str) -> str:
    """Type hints for documentation"""
    return f"Hello, {name}!"

# Checking with isinstance (recommended)
if isinstance(value, (int, float)):
    print("It's a number")
```

---

## Best Practices

### 1. Use Meaningful Names
```python
# ❌ Bad
a = 10
b = "John"

# ✅ Good
user_age = 10
user_name = "John"
```

### 2. Be Consistent with Types
```python
# ❌ Bad - inconsistent types
data = [1, "two", 3.0, None]

# ✅ Good - consistent types
numbers = [1, 2, 3, 4, 5]
names = ["Alice", "Bob", "Charlie"]
```

### 3. Use Type Hints
```python
# ✅ Good practice
def calculate_total(price: float, quantity: int) -> float:
    return price * quantity
```

### 4. Know Mutable vs Immutable
```python
# Immutable types (strings, tuples, ints, floats)
immutable = (1, 2, 3)
# immutable[0] = 5  # ❌ Error!

# Mutable types (lists, dicts, sets)
mutable = [1, 2, 3]
mutable[0] = 5  # ✅ Works!
```

### 5. Avoid Type Ambiguity
```python
# ❌ Confusing
result = 10 / "2"  # Error!

# ✅ Clear
result = 10 / int("2")
```

---

## Summary

| Type | Mutable | Ordered | Unique | Example |
|------|---------|---------|--------|---------|
| int | - | - | - | 42 |
| float | - | - | - | 3.14 |
| str | No | Yes | - | "hello" |
| bool | - | - | - | True |
| list | Yes | Yes | No | [1, 2, 3] |
| tuple | No | Yes | No | (1, 2, 3) |
| dict | Yes | Yes* | Keys | {"a": 1} |
| set | Yes | No | Yes | {1, 2, 3} |

---

## Practice Exercises

1. **Basic Types**
   - Create variables of each basic type
   - Print their types using `type()`

2. **Type Conversion**
   - Convert string "123" to integer
   - Convert integer 456 to string
   - Convert string "3.14" to float

3. **Collections**
   - Create a list of 5 numbers
   - Convert it to a tuple
   - Create a dictionary from the numbers

4. **Mixed Operations**
   - Combine data types in meaningful ways
   - Practice type conversions

---

**Next**: [Operators](operators.md)
