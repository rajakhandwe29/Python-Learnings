# Interview Questions - Beginner Level

Common Python interview questions for beginners.

## Basic Concepts

### 1. What is Python? List its key features.
**Answer**: 
- High-level, interpreted programming language
- Simple, readable syntax
- Dynamically typed
- Multi-paradigm (OOP, functional, procedural)
- Large standard library
- Cross-platform

### 2. What are the differences between Python 2 and Python 3?
**Answer**:
- Print statement vs print function
- String handling (Unicode by default in 3)
- Division operator behavior
- Library differences
- Python 2 is deprecated (end 2020)

### 3. What is PEP 8?
**Answer**: 
- Python Enhancement Proposal 8
- Style guide for Python code
- Recommends 4-space indentation
- Max line length 79 characters
- Improves code readability

## Variables and Data Types

### 4. What are Python's basic data types?
**Answer**:
- int (integers)
- float (decimals)
- str (strings)
- bool (True/False)
- list, tuple, dict, set

### 5. Explain the difference between mutable and immutable types.
**Answer**:
- Mutable: Can be changed after creation (list, dict, set)
- Immutable: Cannot be changed (int, float, str, tuple)

**Example**:
```python
# Mutable
list1 = [1, 2, 3]
list1[0] = 5  # Allowed

# Immutable
str1 = "hello"
str1[0] = "H"  # Error!
```

### 6. What is the difference between = and ==?
**Answer**:
- `=` is assignment operator
- `==` is comparison operator
- `is` checks identity (same object)

## Data Structures

### 7. What is the difference between lists and tuples?
**Answer**:
- Lists are mutable, tuples are immutable
- Lists use [], tuples use ()
- Tuples are faster and can be dictionary keys
- Lists are used when you need modification

### 8. What is a dictionary? How is it different from a list?
**Answer**:
- Dictionary: key-value pairs, unordered (before 3.7)
- List: ordered collection, accessed by index
- Dictionaries are faster for lookups by key

**Example**:
```python
# List - indexed access
numbers = [1, 2, 3]
numbers[0]  # First element

# Dictionary - key access
person = {"name": "John", "age": 25}
person["name"]  # "John"
```

### 9. What are sets? What are their operations?
**Answer**:
- Unordered collection of unique elements
- Operations: union (|), intersection (&), difference (-), symmetric difference (^)

**Example**:
```python
set1 = {1, 2, 3}
set2 = {2, 3, 4}
set1 | set2  # {1, 2, 3, 4}
set1 & set2  # {2, 3}
```

## Control Flow

### 10. What is the difference between break and continue?
**Answer**:
- `break`: Exits the loop completely
- `continue`: Skips current iteration, continues to next

**Example**:
```python
for i in range(5):
    if i == 2:
        break      # Stops loop at i=2
    print(i)  # Prints 0, 1

for i in range(5):
    if i == 2:
        continue   # Skips i=2
    print(i)  # Prints 0, 1, 3, 4
```

### 11. What is the difference between if/elif/else?
**Answer**:
- `if`: Checks condition
- `elif`: "else if" - multiple conditions
- `else`: Default case
- Stops checking once a condition is true

### 12. What is a list comprehension?
**Answer**: Concise way to create lists

**Example**:
```python
# Traditional
squares = []
for x in range(5):
    squares.append(x**2)

# List comprehension
squares = [x**2 for x in range(5)]

# With condition
evens = [x for x in range(10) if x % 2 == 0]
```

## Functions

### 13. What is a function? Explain parameters vs arguments.
**Answer**:
- Function: Reusable block of code
- Parameter: Variable in function definition
- Argument: Actual value passed to function

**Example**:
```python
def greet(name):  # 'name' is parameter
    print(f"Hello, {name}")

greet("John")  # "John" is argument
```

### 14. What is the difference between local and global scope?
**Answer**:
- Local: Variables inside function, only accessible there
- Global: Variables outside function, accessible everywhere
- `global` keyword to modify global variable in function

**Example**:
```python
x = 10  # Global

def func():
    x = 5   # Local x
    print(x)  # 5

print(x)  # 10
```

### 15. What is *args and **kwargs?
**Answer**:
- `*args`: Variable length non-keyword arguments (tuple)
- `**kwargs`: Variable length keyword arguments (dictionary)

**Example**:
```python
def func(*args, **kwargs):
    print(args)    # (1, 2, 3)
    print(kwargs)  # {'name': 'John'}

func(1, 2, 3, name="John")
```

## Strings

### 16. What are string methods? Name a few.
**Answer**: Built-in functions for string manipulation
- `upper()`, `lower()` - Change case
- `split()`, `join()` - Split/combine strings
- `replace()` - Replace substring
- `strip()` - Remove whitespace
- `find()`, `index()` - Find substring

### 17. What is string formatting? Name different ways.
**Answer**:
```python
# Old style
"Hello %s" % "World"

# .format()
"Hello {}".format("World")

# f-strings (preferred)
f"Hello {'World'}"
```

## Operators

### 18. What are comparison operators?
**Answer**: ==, !=, <, >, <=, >=
- Return True or False
- Used in conditionals

### 19. What are logical operators?
**Answer**: and, or, not
- `and`: Both conditions true
- `or`: At least one condition true
- `not`: Negates condition

### 20. What is the modulo operator (%)? How is it useful?
**Answer**: Returns remainder of division
- Check if number is even/odd: `x % 2 == 0`
- Cycle through values: `index % length`
- Find remainder in division

---

## Tips for Interview Success

✅ Know the basics deeply
✅ Be able to write code correctly
✅ Understand when to use which data structure
✅ Know time complexity basics
✅ Practice explaining concepts
✅ Write clean, readable code

---

**Next Level**: [Intermediate Interview Questions](../intermediate-level.md)
