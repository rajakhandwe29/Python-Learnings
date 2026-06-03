# Interview Questions - Intermediate Level

Python interview questions for developers with basic experience.

## Data Structures - Advanced

### 1. Explain the difference between list.copy() and copy.deepcopy()

**Answer**: 
- `list.copy()` creates a shallow copy (first level only)
- `copy.deepcopy()` creates a deep copy (all levels)

**Example**:
```python
import copy

original = [[1, 2], [3, 4]]

# Shallow copy
shallow = original.copy()
shallow[0][0] = 99
print(original)  # [[99, 2], [3, 4]] - Original affected!

# Deep copy
original = [[1, 2], [3, 4]]
deep = copy.deepcopy(original)
deep[0][0] = 99
print(original)  # [[1, 2], [3, 4]] - Original unchanged
```

### 2. When should you use a set instead of a list?

**Answer**: Use sets when:
- You need unique elements only
- Performance matters (faster lookups)
- You need set operations (union, intersection)
- Order doesn't matter

**Example**:
```python
# List - O(n) lookup
users_list = ["Alice", "Bob", "Alice"]
if "Alice" in users_list:  # Scans all elements

# Set - O(1) lookup
users_set = {"Alice", "Bob"}
if "Alice" in users_set:  # Direct lookup (faster!)

# Remove duplicates
users = ["Alice", "Bob", "Alice", "Charlie", "Bob"]
unique_users = list(set(users))
```

### 3. What are the advantages of using defaultdict?

**Answer**: Automatically initializes missing keys with default value

**Example**:
```python
from collections import defaultdict

# Without defaultdict
count_dict = {}
for word in ["apple", "banana", "apple"]:
    if word in count_dict:
        count_dict[word] += 1
    else:
        count_dict[word] = 1

# With defaultdict
count_dict = defaultdict(int)
for word in ["apple", "banana", "apple"]:
    count_dict[word] += 1

print(count_dict)  # defaultdict(<class 'int'>, {'apple': 2, 'banana': 1})
```

### 4. How do you merge two dictionaries?

**Answer**: Multiple ways to merge dictionaries

**Example**:
```python
dict1 = {"a": 1, "b": 2}
dict2 = {"c": 3, "d": 4}

# Method 1: Update (modifies in place)
dict1.update(dict2)
print(dict1)  # {"a": 1, "b": 2, "c": 3, "d": 4}

# Method 2: Unpacking (Python 3.5+)
merged = {**dict1, **dict2}

# Method 3: merge function (Python 3.9+)
merged = dict1 | dict2

# For nested dicts, use deepcopy
import copy
dict1 = {"settings": {"theme": "dark"}}
dict2 = {"settings": {"language": "en"}}
merged = copy.deepcopy(dict1)
merged["settings"].update(dict2["settings"])
```

---

## Object-Oriented Programming

### 5. What is the difference between instance variables and class variables?

**Answer**:
- Instance variables: Unique to each object
- Class variables: Shared by all instances

**Example**:
```python
class Car:
    wheels = 4  # Class variable (shared)
    
    def __init__(self, color):
        self.color = color  # Instance variable (unique)

car1 = Car("red")
car2 = Car("blue")

print(car1.color)      # "red"
print(car2.color)      # "blue"
print(Car.wheels)      # 4
print(car1.wheels)     # 4 (accessed through instance)
```

### 6. Explain __init__, __str__, and __repr__

**Answer**:
- `__init__`: Constructor, initializes object
- `__str__`: User-friendly string representation
- `__repr__`: Developer-friendly representation

**Example**:
```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def __str__(self):
        return f"{self.name} ({self.age} years old)"
    
    def __repr__(self):
        return f"Person(name='{self.name}', age={self.age})"

person = Person("Alice", 25)
print(str(person))    # Alice (25 years old)
print(repr(person))   # Person(name='Alice', age=25)
```

### 7. What is inheritance and method overriding?

**Answer**: Inheritance allows classes to inherit from other classes; method overriding replaces parent methods

**Example**:
```python
class Animal:
    def speak(self):
        return "Some sound"

class Dog(Animal):
    def speak(self):  # Override parent method
        return "Woof!"

class Cat(Animal):
    def speak(self):
        return "Meow!"

dog = Dog()
cat = Cat()
print(dog.speak())    # "Woof!"
print(cat.speak())    # "Meow!"
```

### 8. What is super() and when to use it?

**Answer**: Calls parent class method, useful for extending functionality

**Example**:
```python
class Animal:
    def __init__(self, name):
        self.name = name
    
    def speak(self):
        return f"{self.name} makes a sound"

class Dog(Animal):
    def __init__(self, name, breed):
        super().__init__(name)  # Call parent __init__
        self.breed = breed
    
    def speak(self):
        parent_speak = super().speak()  # Call parent method
        return f"{parent_speak} - Woof!"

dog = Dog("Buddy", "Golden Retriever")
print(dog.speak())  # Buddy makes a sound - Woof!
```

---

## Functional Programming

### 9. What are lambda functions and when to use them?

**Answer**: Anonymous functions for short, simple operations

**Example**:
```python
# Instead of defining a function
def double(x):
    return x * 2

# Use lambda
double = lambda x: x * 2

# Most useful with map, filter, sorted
numbers = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x ** 2, numbers))  # [1, 4, 9, 16, 25]

# Sort by custom key
people = [("Alice", 25), ("Bob", 20), ("Charlie", 30)]
sorted_by_age = sorted(people, key=lambda x: x[1])
# [("Bob", 20), ("Alice", 25), ("Charlie", 30)]
```

### 10. Explain map(), filter(), and reduce()

**Answer**: Functional programming tools for processing sequences

**Example**:
```python
from functools import reduce

numbers = [1, 2, 3, 4, 5]

# map - transform each element
squared = list(map(lambda x: x ** 2, numbers))
# [1, 4, 9, 16, 25]

# filter - keep elements matching condition
evens = list(filter(lambda x: x % 2 == 0, numbers))
# [2, 4]

# reduce - combine elements into single value
product = reduce(lambda x, y: x * y, numbers)
# 1 * 2 * 3 * 4 * 5 = 120

# Better alternatives in modern Python
squared = [x ** 2 for x in numbers]
evens = [x for x in numbers if x % 2 == 0]
product = sum(x for x in numbers if x > 0)  # Use built-in when possible
```

### 11. What are decorators?

**Answer**: Functions that modify other functions or classes

**Example**:
```python
def timing_decorator(func):
    import time
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f"Took {end - start:.4f} seconds")
        return result
    return wrapper

@timing_decorator
def slow_function():
    import time
    time.sleep(1)
    return "Done"

slow_function()  # Prints execution time
```

### 12. What are generators and yield?

**Answer**: Generators produce values on-demand, saving memory

**Example**:
```python
# List - loads all into memory
def range_list(n):
    result = []
    for i in range(n):
        result.append(i)
    return result

# Generator - produces on-demand
def range_gen(n):
    for i in range(n):
        yield i

# Usage
for i in range_gen(5):
    print(i)  # Prints 0, 1, 2, 3, 4

# Generator expression
squares = (x ** 2 for x in range(5))  # Generator object
print(next(squares))  # 0
print(next(squares))  # 1
```

---

## Error Handling

### 13. What's the difference between ValueError and TypeError?

**Answer**:
- TypeError: Wrong type for operation
- ValueError: Correct type but invalid value

**Example**:
```python
# TypeError - wrong type
try:
    result = "5" + 5
except TypeError as e:
    print(f"TypeError: {e}")  # unsupported operand type(s)

# ValueError - wrong value
try:
    age = int("twenty")
except ValueError as e:
    print(f"ValueError: {e}")  # invalid literal for int()
```

### 14. When to use try-except-else-finally?

**Answer**: 
- try: Code that might fail
- except: Handle errors
- else: Code if no error
- finally: Cleanup code always runs

**Example**:
```python
try:
    file = open("data.txt", "r")
    data = file.read()
except FileNotFoundError:
    print("File not found")
except Exception as e:
    print(f"Error: {e}")
else:
    print("File read successfully")
    process_data(data)
finally:
    file.close()  # Always runs
```

---

## Advanced Topics

### 15. What is a context manager (with statement)?

**Answer**: Automatically handles setup and cleanup

**Example**:
```python
# Without context manager
file = open("data.txt")
try:
    data = file.read()
finally:
    file.close()

# With context manager
with open("data.txt") as file:
    data = file.read()
# File automatically closed

# Create your own
class MyContext:
    def __enter__(self):
        print("Entering")
        return self
    
    def __exit__(self, exc_type, exc_val, exc_tb):
        print("Exiting")

with MyContext() as ctx:
    print("Inside")
```

### 16. Explain *args and **kwargs

**Answer**: 
- *args: Variable positional arguments (tuple)
- **kwargs: Variable keyword arguments (dict)

**Example**:
```python
def print_all(*args, **kwargs):
    print(f"args: {args}")        # (1, 2, 3)
    print(f"kwargs: {kwargs}")    # {'name': 'Alice', 'age': 25}

print_all(1, 2, 3, name="Alice", age=25)

# Unpacking
def add(a, b, c):
    return a + b + c

numbers = [1, 2, 3]
print(add(*numbers))  # 6

params = {"a": 1, "b": 2, "c": 3}
print(add(**params))  # 6
```

### 17. What is list slicing and how does it work?

**Answer**: Extracts part of sequence using [start:stop:step]

**Example**:
```python
items = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

print(items[2:5])     # [2, 3, 4]
print(items[:5])      # [0, 1, 2, 3, 4]
print(items[5:])      # [5, 6, 7, 8, 9]
print(items[::2])     # [0, 2, 4, 6, 8]
print(items[::-1])    # [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]

# Assignment with slice
items[1:4] = [10, 20, 30]
print(items)  # [0, 10, 20, 30, 5, 6, 7, 8, 9]
```

### 18. What is memoization and how to implement it?

**Answer**: Cache function results to avoid recomputation

**Example**:
```python
from functools import lru_cache

# Without memoization - slow for recursive calls
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n-1) + fibonacci(n-2)

# With memoization - fast
@lru_cache(maxsize=None)
def fibonacci_fast(n):
    if n <= 1:
        return n
    return fibonacci_fast(n-1) + fibonacci_fast(n-2)

print(fibonacci_fast(35))  # Much faster!
```

### 19. Explain the GIL (Global Interpreter Lock)

**Answer**: Allows only one thread to execute Python bytecode at a time

**Example**:
```python
import threading

# CPU-bound task - GIL limits performance
def cpu_intensive():
    total = 0
    for i in range(100000000):
        total += i
    return total

# Use multiprocessing for CPU-bound tasks
from multiprocessing import Pool

with Pool(4) as p:
    results = p.map(cpu_intensive, range(4))

# Use threading for I/O-bound tasks
import requests

threads = []
for url in urls:
    t = threading.Thread(target=requests.get, args=(url,))
    threads.append(t)
    t.start()
```

### 20. What is the difference between == and is?

**Answer**:
- ==: Checks value equality
- is: Checks object identity (same reference)

**Example**:
```python
# Value equality
a = [1, 2, 3]
b = [1, 2, 3]
print(a == b)  # True (same contents)
print(a is b)  # False (different objects)

# Identity (important for None)
value = None
print(value is None)     # True (correct way)
print(value == None)     # True (works but not Pythonic)

# String interning
x = "hello"
y = "hello"
print(x is y)  # Usually True (Python optimization)
```

---

## Tips for Interview Success

✅ Understand WHY, not just HOW
✅ Explain your reasoning
✅ Write clean, readable code
✅ Handle edge cases
✅ Optimize when asked
✅ Ask clarifying questions
✅ Test your code mentally

---

**Next Level**: [Advanced Interview Questions](../advanced-level.md)
