# Polymorphism in Python: A Comprehensive Guide

## Table of Contents
1. [Introduction](#introduction)
2. [Method Overriding](#method-overriding)
3. [Duck Typing](#duck-typing)
4. [Operator Overloading](#operator-overloading)
5. [Function Overloading](#function-overloading)
6. [Polymorphic Collections](#polymorphic-collections)
7. [Runtime Type Checking](#runtime-type-checking)
8. [Practical Examples](#practical-examples)
9. [Common Mistakes](#common-mistakes)
10. [Best Practices](#best-practices)
11. [Summary](#summary)

## Introduction

Polymorphism means "many forms." In Python, it refers to the ability of objects to take multiple forms or for functions to work with objects of different types. Python achieves polymorphism through method overriding, duck typing, and operator overloading.

### Why Polymorphism Matters

Polymorphism enables:
- Writing flexible, generic code
- Using objects interchangeably
- Extending behavior without modifying existing code
- Dynamic behavior at runtime
- Clean interfaces regardless of implementation

### Quick Example

```python
class Shape:
    def area(self):
        pass

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius
    
    def area(self):
        return 3.14159 * self.radius ** 2

class Square(Shape):
    def __init__(self, side):
        self.side = side
    
    def area(self):
        return self.side ** 2

def print_areas(shapes):
    for shape in shapes:
        print(f"Area: {shape.area():.2f}")

# Polymorphism in action
shapes = [Circle(5), Square(10)]
print_areas(shapes)
# Output:
# Area: 78.54
# Area: 100.00
```

## Method Overriding

### Overriding Parent Methods

```python
class Animal:
    def speak(self):
        return "Some generic sound"
    
    def move(self):
        return "Moving..."

class Dog(Animal):
    def speak(self):
        return "Woof! Woof!"  # Override parent method

class Cat(Animal):
    def speak(self):
        return "Meow..."  # Override parent method

# Each class provides its own implementation
dog = Dog()
cat = Cat()
animal = Animal()

print(dog.speak())     # Output: Woof! Woof!
print(cat.speak())     # Output: Meow...
print(animal.speak())  # Output: Some generic sound

# Not-overridden methods use parent implementation
print(dog.move())      # Output: Moving...
print(cat.move())      # Output: Moving...
```

### Polymorphic Behavior

```python
def animal_sound(animal):
    """Works with any animal object"""
    print(animal.speak())

class Dog:
    def speak(self):
        return "Woof!"

class Cat:
    def speak(self):
        return "Meow!"

class Cow:
    def speak(self):
        return "Moo!"

# Same function works with different types
animal_sound(Dog())  # Output: Woof!
animal_sound(Cat())  # Output: Meow!
animal_sound(Cow())  # Output: Moo!
```

## Duck Typing

### "If it looks like a duck and quacks like a duck..."

```python
# Duck typing: don't check types, check behavior
def use_speaker(speaker):
    """Works with any object that has a speak() method"""
    print(speaker.speak())

# Different classes, same interface
class Dog:
    def speak(self):
        return "Woof!"

class Parrot:
    def speak(self):
        return "Polly want a cracker!"

class Robot:
    def speak(self):
        return "Beep boop!"

# Duck typing allows using these interchangeably
use_speaker(Dog())     # Output: Woof!
use_speaker(Parrot())  # Output: Polly want a cracker!
use_speaker(Robot())   # Output: Beep boop!

# No inheritance hierarchy needed!
```

### Practical Duck Typing

```python
# This function works with any iterable
def process_items(items):
    for item in items:
        print(f"Processing: {item}")

# Works with lists
process_items([1, 2, 3])

# Works with tuples
process_items((4, 5, 6))

# Works with strings
process_items("abc")

# Works with sets
process_items({7, 8, 9})

# Works with any custom iterable
class CustomIterable:
    def __iter__(self):
        return iter([10, 11, 12])

process_items(CustomIterable())
```

## Operator Overloading

### Common Operators

```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    
    # Arithmetic operators
    def __add__(self, other):
        return Vector(self.x + other.x, self.y + other.y)
    
    def __sub__(self, other):
        return Vector(self.x - other.x, self.y - other.y)
    
    def __mul__(self, scalar):
        return Vector(self.x * scalar, self.y * scalar)
    
    # Comparison operators
    def __eq__(self, other):
        return self.x == other.x and self.y == other.y
    
    def __lt__(self, other):
        return (self.x ** 2 + self.y ** 2) < (other.x ** 2 + other.y ** 2)
    
    # String representation
    def __repr__(self):
        return f"Vector({self.x}, {self.y})"

v1 = Vector(1, 2)
v2 = Vector(3, 4)

print(v1 + v2)   # Output: Vector(4, 6)
print(v1 - v2)   # Output: Vector(-2, -2)
print(v1 * 2)    # Output: Vector(2, 4)
print(v1 == Vector(1, 2))  # Output: True
print(v1 < v2)   # Output: True
```

### Container Operators

```python
class ShoppingCart:
    def __init__(self):
        self.items = []
    
    def __len__(self):
        return len(self.items)
    
    def __getitem__(self, index):
        return self.items[index]
    
    def __setitem__(self, index, value):
        self.items[index] = value
    
    def __contains__(self, item):
        return item in self.items
    
    def __add__(self, item):
        self.items.append(item)
        return self
    
    def __repr__(self):
        return f"ShoppingCart({self.items})"

cart = ShoppingCart()
cart + "Apple" + "Banana" + "Orange"

print(len(cart))              # Output: 3
print(cart[0])                # Output: Apple
print("Banana" in cart)       # Output: True
print(cart)                   # Output: ShoppingCart(['Apple', 'Banana', 'Orange'])
```

## Function Overloading

### Default Arguments

```python
class FileProcessor:
    def read(self, filename, encoding="utf-8"):
        return f"Reading {filename} with {encoding}"
    
    def write(self, filename, data="", encoding="utf-8"):
        return f"Writing to {filename} with {encoding}"

processor = FileProcessor()
print(processor.read("file.txt"))
print(processor.read("file.txt", "latin-1"))
print(processor.write("output.txt"))
print(processor.write("output.txt", "Hello"))
```

### Variable Arguments

```python
def print_values(*args, **kwargs):
    """Print positional and keyword arguments"""
    print(f"Positional args: {args}")
    print(f"Keyword args: {kwargs}")

print_values(1, 2, 3, name="Alice", age=30)
# Output:
# Positional args: (1, 2, 3)
# Keyword args: {'name': 'Alice', 'age': 30}

def sum_all(*numbers):
    """Sum any number of arguments"""
    return sum(numbers)

print(sum_all(1, 2, 3, 4, 5))  # Output: 15
print(sum_all(10, 20))          # Output: 30
```

### Method Dispatch

```python
from functools import singledispatch

@singledispatch
def process(data):
    """Default processor"""
    raise NotImplementedError(f"Cannot process {type(data)}")

@process.register(int)
def _(data):
    return f"Processing integer: {data * 2}"

@process.register(str)
def _(data):
    return f"Processing string: {data.upper()}"

@process.register(list)
def _(data):
    return f"Processing list: {len(data)} items"

print(process(5))          # Output: Processing integer: 10
print(process("hello"))    # Output: Processing string: HELLO
print(process([1, 2, 3]))  # Output: Processing list: 3 items
```

## Polymorphic Collections

### Mixed Type Collections

```python
class Musician:
    def perform(self):
        pass

class Guitarist(Musician):
    def perform(self):
        return "Playing guitar..."

class Pianist(Musician):
    def perform(self):
        return "Playing piano..."

class Drummer(Musician):
    def perform(self):
        return "Beating drums..."

def orchestra_performance(musicians):
    """Polymorphic function - works with any musician"""
    print("=== Orchestra Performance ===")
    for musician in musicians:
        print(musician.perform())

# Mixed collection of different musician types
musicians = [
    Guitarist(),
    Pianist(),
    Drummer(),
    Guitarist(),
    Pianist()
]

orchestra_performance(musicians)
# Output:
# === Orchestra Performance ===
# Playing guitar...
# Playing piano...
# Beating drums...
# Playing guitar...
# Playing piano...
```

### Polymorphic Data Processing

```python
class DataSource:
    def fetch(self):
        pass

class APISource(DataSource):
    def fetch(self):
        return "Data from API"

class DatabaseSource(DataSource):
    def fetch(self):
        return "Data from Database"

class FileSource(DataSource):
    def fetch(self):
        return "Data from File"

def data_pipeline(sources):
    """Works with any data source"""
    results = []
    for source in sources:
        results.append(source.fetch())
    return results

# Use different sources
sources = [
    APISource(),
    DatabaseSource(),
    FileSource(),
    APISource()
]

data = data_pipeline(sources)
for item in data:
    print(item)
```

## Runtime Type Checking

### Type Checking Methods

```python
def process(obj):
    """Check object type at runtime"""
    if isinstance(obj, int):
        return f"Integer: {obj * 2}"
    elif isinstance(obj, str):
        return f"String: {obj.upper()}"
    elif isinstance(obj, list):
        return f"List with {len(obj)} items"
    else:
        return f"Unknown type: {type(obj)}"

print(process(42))
print(process("hello"))
print(process([1, 2, 3]))

class Parent:
    pass

class Child(Parent):
    pass

obj = Child()
print(isinstance(obj, Child))   # Output: True
print(isinstance(obj, Parent))  # Output: True
print(isinstance(obj, object))  # Output: True
```

### Duck Typing vs Type Checking

```python
# DUCK TYPING - Pythonic approach
def get_length_duck_typing(obj):
    """Assumes object has __len__ method"""
    return len(obj)

# Works with anything that has __len__
print(get_length_duck_typing([1, 2, 3]))  # Output: 3
print(get_length_duck_typing("hello"))    # Output: 5
print(get_length_duck_typing({1, 2, 3}))  # Output: 3

# TYPE CHECKING - Less Pythonic
def get_length_with_type_check(obj):
    """Check specific types"""
    if isinstance(obj, (list, str, set)):
        return len(obj)
    raise TypeError(f"Cannot get length of {type(obj)}")

# More restrictive, less flexible
```

## Practical Examples

### Payment Processing

```python
class PaymentProcessor:
    def process_payment(self, method):
        """Process payment using any method"""
        return method.pay()

class CreditCard:
    def pay(self):
        return "Processing credit card payment..."

class PayPal:
    def pay(self):
        return "Processing PayPal payment..."

class Bitcoin:
    def pay(self):
        return "Processing Bitcoin payment..."

processor = PaymentProcessor()

methods = [
    CreditCard(),
    PayPal(),
    Bitcoin(),
    CreditCard()
]

for method in methods:
    print(processor.process_payment(method))
```

### Database Abstraction

```python
from abc import ABC, abstractmethod

class Database(ABC):
    @abstractmethod
    def connect(self):
        pass
    
    @abstractmethod
    def query(self, sql):
        pass
    
    @abstractmethod
    def close(self):
        pass

class MySQL(Database):
    def connect(self):
        return "Connected to MySQL"
    
    def query(self, sql):
        return f"MySQL: {sql}"
    
    def close(self):
        return "MySQL connection closed"

class PostgreSQL(Database):
    def connect(self):
        return "Connected to PostgreSQL"
    
    def query(self, sql):
        return f"PostgreSQL: {sql}"
    
    def close(self):
        return "PostgreSQL connection closed"

class MongoDB(Database):
    def connect(self):
        return "Connected to MongoDB"
    
    def query(self, sql):
        return f"MongoDB: {sql}"
    
    def close(self):
        return "MongoDB connection closed"

def database_client(db):
    """Works with any database"""
    print(db.connect())
    print(db.query("SELECT * FROM users"))
    print(db.close())

databases = [MySQL(), PostgreSQL(), MongoDB()]

for db in databases:
    database_client(db)
    print()
```

## Common Mistakes

### Mistake 1: Not Understanding Duck Typing

```python
# WRONG - type checking when not needed
def process_iterable(obj):
    if isinstance(obj, list):
        return sum(obj)
    elif isinstance(obj, tuple):
        return sum(obj)
    # Won't work with custom iterables!

# CORRECT - use duck typing
def process_iterable_good(obj):
    return sum(obj)  # Works with any iterable

# Works with custom class
class CustomIterable:
    def __iter__(self):
        return iter([1, 2, 3])

print(process_iterable_good(CustomIterable()))  # Output: 6
```

### Mistake 2: Broken Liskov Substitution Principle

```python
# WRONG - derived class breaks expected behavior
class Bird:
    def fly(self):
        return "Flying at 100km/h"

class Penguin(Bird):
    def fly(self):
        raise NotImplementedError("Penguins can't fly!")

# This breaks LSP
def make_bird_fly(bird):
    return bird.fly()

# make_bird_fly(Penguin())  # Will crash!

# CORRECT - proper inheritance hierarchy
class Bird:
    def move(self):
        return "Moving..."

class FlyingBird(Bird):
    def fly(self):
        return "Flying..."

class SwimmingBird(Bird):
    def swim(self):
        return "Swimming..."

class Penguin(SwimmingBird):
    def swim(self):
        return "Swimming at 10km/h"
```

### Mistake 3: Overloading Operators Inconsistently

```python
# WRONG - inconsistent operator behavior
class WeirdNumber:
    def __init__(self, value):
        self.value = value
    
    def __add__(self, other):
        # Addition returns multiplication?!
        return WeirdNumber(self.value * other.value)
    
    def __mul__(self, other):
        # Multiplication returns addition?!
        return WeirdNumber(self.value + other.value)

# This violates principle of least surprise

# CORRECT - operators behave as expected
class Number:
    def __init__(self, value):
        self.value = value
    
    def __add__(self, other):
        return Number(self.value + other.value)
    
    def __mul__(self, other):
        return Number(self.value * other.value)
    
    def __repr__(self):
        return f"Number({self.value})"
```

## Best Practices

### 1. Embrace Duck Typing

```python
# GOOD - flexible, Pythonic
def process_items(items):
    for item in items:
        print(item)

# Works with lists, tuples, strings, generators, custom iterables

# LESS GOOD - rigid type checking
def process_items_strict(items):
    if not isinstance(items, list):
        raise TypeError("Must be a list")
    # Only works with lists
```

### 2. Keep Polymorphic Interfaces Consistent

```python
# GOOD - consistent interface across implementations
class DataStore:
    def save(self, key, data):
        raise NotImplementedError
    
    def load(self, key):
        raise NotImplementedError

class MemoryStore(DataStore):
    def save(self, key, data):
        # Consistent implementation
        pass
    
    def load(self, key):
        # Consistent implementation
        pass
```

### 3. Use Abstract Base Classes

```python
from abc import ABC, abstractmethod

# GOOD - enforces implementation
class Processor(ABC):
    @abstractmethod
    def process(self, data):
        pass
```

## Summary

| Concept | Description | Example |
|---------|-------------|---------|
| **Polymorphism** | Objects take multiple forms | Different classes, same interface |
| **Duck Typing** | Behavior matters more than type | `len(obj)` works with any iterable |
| **Method Overriding** | Subclass replaces parent method | `def method(self): ...` |
| **Operator Overloading** | Custom operator behavior | `def __add__(self, other):` |
| **Polymorphic Collections** | Mixed type lists | `[Dog(), Cat(), Bird()]` |
| **Runtime Type Checking** | Check types at runtime | `isinstance(obj, Class)` |

### Key Takeaways

1. **Python is polymorphic by nature** - leverage it
2. **Duck typing is Pythonic** - check behavior, not type
3. **Consistent interfaces enable polymorphism** - same method names
4. **Override methods in subclasses** - customize behavior
5. **Operator overloading adds expressiveness** - use judiciously
6. **Polymorphic collections are powerful** - mix types freely
7. **Follow SOLID principles** - especially Liskov Substitution

### Practice Exercises

1. Create a shape system with polymorphic area calculation
2. Build a notification system with multiple notification types
3. Implement a logger that works with file, console, and email outputs
4. Create a vehicle system with different movement behaviors
5. Build a payment processor supporting multiple payment methods

---

**Next:** Learn encapsulation to protect object state and control access to attributes and methods.
