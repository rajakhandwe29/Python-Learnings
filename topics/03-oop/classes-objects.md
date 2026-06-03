# Classes and Objects in Python: A Comprehensive Guide

## Table of Contents
1. [Introduction](#introduction)
2. [Class Definition](#class-definition)
3. [Attributes](#attributes)
4. [Methods](#methods)
5. [The __init__ Constructor](#the-__init__-constructor)
6. [Instance vs Class Attributes](#instance-vs-class-attributes)
7. [Special Methods](#special-methods)
8. [Object Lifecycle](#object-lifecycle)
9. [Practical Examples](#practical-examples)
10. [Common Mistakes](#common-mistakes)
11. [Best Practices](#best-practices)
12. [Summary](#summary)

## Introduction

Classes are blueprints for creating objects in Python. An object is an instance of a class, containing both data (attributes) and behavior (methods). Object-oriented programming (OOP) is a paradigm that allows you to structure code around objects and their interactions.

### Why Classes Matter

Classes enable:
- Code organization and modularity
- Code reusability through inheritance
- Data encapsulation and abstraction
- Polymorphic behavior
- Real-world problem modeling

### Quick Example

```python
class Dog:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def bark(self):
        return f"{self.name} says: Woof!"
    
    def get_age(self):
        return self.age

# Create instances
dog1 = Dog("Buddy", 3)
dog2 = Dog("Max", 5)

print(dog1.bark())          # Output: Buddy says: Woof!
print(f"Max is {dog2.age} years old")  # Output: Max is 5 years old
```

## Class Definition

### Basic Syntax

```python
# Simple class definition
class Person:
    pass

# Create an instance
person = Person()
print(type(person))  # Output: <class '__main__.Person'>

# Class with attributes
class Car:
    color = "blue"  # Class attribute
    wheels = 4      # Class attribute

car = Car()
print(car.color)   # Output: blue
print(car.wheels)  # Output: 4
```

### Naming Conventions

```python
# Class names use PascalCase (CapitalizeFirstLetter)
class MyClass:
    pass

class DatabaseConnection:
    pass

# Method names use lowercase with underscores
class Calculator:
    def add_numbers(self):
        pass
    
    def multiply_values(self):
        pass

# Constants use UPPERCASE with underscores
class Config:
    MAX_RETRIES = 3
    TIMEOUT = 30
    API_KEY = "secret123"
```

## Attributes

### Instance Attributes

Instance attributes are specific to each object instance:

```python
class Student:
    def __init__(self, name, grade):
        self.name = name    # Instance attribute
        self.grade = grade  # Instance attribute

# Each student has their own attributes
student1 = Student("Alice", "A")
student2 = Student("Bob", "B")

print(student1.name)   # Output: Alice
print(student2.name)   # Output: Bob
print(student1.grade)  # Output: A

# Modifying instance attributes
student1.grade = "A+"
print(student1.grade)  # Output: A+
print(student2.grade)  # Output: B (unchanged)
```

### Class Attributes

Class attributes are shared among all instances:

```python
class Vehicle:
    vehicle_count = 0  # Class attribute
    
    def __init__(self, make):
        self.make = make  # Instance attribute
        Vehicle.vehicle_count += 1

car1 = Vehicle("Toyota")
car2 = Vehicle("Honda")
car3 = Vehicle("Ford")

print(Vehicle.vehicle_count)  # Output: 3
print(car1.vehicle_count)     # Output: 3 (via instance)

# Modifying class attribute
Vehicle.vehicle_count = 100
print(car1.vehicle_count)     # Output: 100 (all instances see this)
```

### Dynamic Attributes

Python allows adding attributes dynamically:

```python
class DynamicClass:
    pass

obj = DynamicClass()
obj.name = "Dynamic"      # Add new attribute
obj.value = 42

print(obj.name)           # Output: Dynamic
print(obj.value)          # Output: 42

# Access non-existent attribute raises AttributeError
try:
    print(obj.nonexistent)
except AttributeError:
    print("Attribute does not exist")

# Use hasattr to check
if hasattr(obj, "name"):
    print(obj.name)
else:
    print("Attribute does not exist")
```

## Methods

### Instance Methods

Instance methods operate on instance data:

```python
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height
    
    def area(self):
        """Calculate rectangle area"""
        return self.width * self.height
    
    def perimeter(self):
        """Calculate rectangle perimeter"""
        return 2 * (self.width + self.height)
    
    def scale(self, factor):
        """Scale rectangle by factor"""
        self.width *= factor
        self.height *= factor

rect = Rectangle(10, 5)
print(rect.area())        # Output: 50
print(rect.perimeter())   # Output: 30

rect.scale(2)
print(rect.area())        # Output: 200
```

### Class Methods

Class methods work with class-level data:

```python
class CircleCounter:
    circle_count = 0
    
    def __init__(self, radius):
        self.radius = radius
        CircleCounter.circle_count += 1
    
    @classmethod
    def get_count(cls):
        """Return total number of circles created"""
        return cls.circle_count
    
    @classmethod
    def reset_count(cls):
        """Reset the counter"""
        cls.circle_count = 0

circle1 = CircleCounter(5)
circle2 = CircleCounter(3)
circle3 = CircleCounter(7)

print(CircleCounter.get_count())  # Output: 3

CircleCounter.reset_count()
print(CircleCounter.get_count())  # Output: 0
```

### Static Methods

Static methods don't access instance or class data:

```python
class Math:
    @staticmethod
    def add(a, b):
        """Add two numbers"""
        return a + b
    
    @staticmethod
    def multiply(a, b):
        """Multiply two numbers"""
        return a * b
    
    @staticmethod
    def is_even(number):
        """Check if number is even"""
        return number % 2 == 0

# Call without creating instance
print(Math.add(5, 3))           # Output: 8
print(Math.multiply(4, 7))      # Output: 28
print(Math.is_even(10))         # Output: True
print(Math.is_even(7))          # Output: False
```

### Property Methods

Properties provide getter/setter functionality:

```python
class Temperature:
    def __init__(self, celsius):
        self._celsius = celsius  # Private by convention
    
    @property
    def celsius(self):
        """Get temperature in Celsius"""
        return self._celsius
    
    @celsius.setter
    def celsius(self, value):
        """Set temperature in Celsius"""
        if value < -273.15:
            raise ValueError("Temperature cannot be below absolute zero")
        self._celsius = value
    
    @property
    def fahrenheit(self):
        """Get temperature in Fahrenheit"""
        return (self._celsius * 9/5) + 32
    
    @fahrenheit.setter
    def fahrenheit(self, value):
        """Set temperature in Fahrenheit"""
        self._celsius = (value - 32) * 5/9

temp = Temperature(0)
print(temp.celsius)      # Output: 0
print(temp.fahrenheit)   # Output: 32.0

temp.celsius = 100
print(temp.fahrenheit)   # Output: 212.0

temp.fahrenheit = 32
print(temp.celsius)      # Output: 0.0
```

## The __init__ Constructor

### Constructor Basics

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
        print(f"Person {name} created")

person = Person("Alice", 30)
# Output: Person Alice created

# Arguments are required
try:
    person = Person("Bob")  # Missing age argument
except TypeError:
    print("Missing required argument")
```

### Default Arguments

```python
class Configuration:
    def __init__(self, host="localhost", port=8000, debug=False):
        self.host = host
        self.port = port
        self.debug = debug

# Various ways to instantiate
config1 = Configuration()
print(f"{config1.host}:{config1.port}, debug={config1.debug}")
# Output: localhost:8000, debug=False

config2 = Configuration("example.com", 3000)
print(f"{config2.host}:{config2.port}, debug={config2.debug}")
# Output: example.com:3000, debug=False

config3 = Configuration(debug=True)
print(f"{config3.host}:{config3.port}, debug={config3.debug}")
# Output: localhost:8000, debug=True
```

### Validation in Constructor

```python
class User:
    def __init__(self, username, email, age):
        if not username or len(username) < 3:
            raise ValueError("Username must be at least 3 characters")
        if "@" not in email:
            raise ValueError("Invalid email format")
        if age < 0 or age > 150:
            raise ValueError("Invalid age")
        
        self.username = username
        self.email = email
        self.age = age

# Valid user
user = User("alice_wonderland", "alice@example.com", 25)
print(f"User: {user.username}")

# Invalid user
try:
    bad_user = User("ab", "invalid", -5)
except ValueError as e:
    print(f"Error: {e}")  # Output: Error: Username must be at least 3 characters
```

## Instance vs Class Attributes

### Understanding the Difference

```python
class Counter:
    global_count = 0  # Class attribute - shared by all instances
    
    def __init__(self):
        self.local_count = 0  # Instance attribute - unique per instance
        Counter.global_count += 1

# Create instances
c1 = Counter()
c2 = Counter()
c3 = Counter()

# Global count is shared
print(Counter.global_count)  # Output: 3
print(c1.local_count)        # Output: 0
print(c2.local_count)        # Output: 0

# Modify instance attributes
c1.local_count = 10
print(c1.local_count)        # Output: 10
print(c2.local_count)        # Output: 0 (unchanged)

# Modifying class attribute affects all instances
Counter.global_count = 100
print(c1.global_count)       # Output: 100
print(c2.global_count)       # Output: 100
```

## Special Methods

### String Representation

```python
class Book:
    def __init__(self, title, author, pages):
        self.title = title
        self.author = author
        self.pages = pages
    
    def __str__(self):
        """User-friendly string representation"""
        return f'"{self.title}" by {self.author}'
    
    def __repr__(self):
        """Developer-friendly representation"""
        return f"Book('{self.title}', '{self.author}', {self.pages})"
    
    def __len__(self):
        """Return length (number of pages)"""
        return self.pages

book = Book("Python Mastery", "John Doe", 450)

# __str__ is used by print()
print(book)  # Output: "Python Mastery" by John Doe

# __repr__ is used in console
print(repr(book))  # Output: Book('Python Mastery', 'John Doe', 450)

# __len__ is used by len()
print(len(book))  # Output: 450
```

### Operator Overloading

```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    
    def __add__(self, other):
        """Add two vectors"""
        return Vector(self.x + other.x, self.y + other.y)
    
    def __sub__(self, other):
        """Subtract two vectors"""
        return Vector(self.x - other.x, self.y - other.y)
    
    def __mul__(self, scalar):
        """Multiply vector by scalar"""
        return Vector(self.x * scalar, self.y * scalar)
    
    def __eq__(self, other):
        """Check equality"""
        return self.x == other.x and self.y == other.y
    
    def __repr__(self):
        return f"Vector({self.x}, {self.y})"

v1 = Vector(1, 2)
v2 = Vector(3, 4)

print(v1 + v2)      # Output: Vector(4, 6)
print(v1 - v2)      # Output: Vector(-2, -2)
print(v1 * 2)       # Output: Vector(2, 4)
print(v1 == Vector(1, 2))  # Output: True
```

### Comparison Methods

```python
class Student:
    def __init__(self, name, gpa):
        self.name = name
        self.gpa = gpa
    
    def __lt__(self, other):
        """Less than comparison"""
        return self.gpa < other.gpa
    
    def __le__(self, other):
        """Less than or equal"""
        return self.gpa <= other.gpa
    
    def __gt__(self, other):
        """Greater than"""
        return self.gpa > other.gpa
    
    def __ge__(self, other):
        """Greater than or equal"""
        return self.gpa >= other.gpa
    
    def __repr__(self):
        return f"Student('{self.name}', {self.gpa})"

alice = Student("Alice", 3.9)
bob = Student("Bob", 3.5)
charlie = Student("Charlie", 3.9)

print(bob < alice)       # Output: True
print(alice > bob)       # Output: True
print(alice >= charlie)  # Output: True

# Sort students by GPA
students = [alice, bob, charlie]
sorted_students = sorted(students)
print(sorted_students)
# Output: [Student('Bob', 3.5), Student('Charlie', 3.9), Student('Alice', 3.9)]
```

## Object Lifecycle

### Creation and Initialization

```python
class FileHandler:
    def __init__(self, filename):
        print(f"__init__: Initializing with {filename}")
        self.filename = filename
        self.file_object = None

    def open(self):
        print(f"open: Opening {self.filename}")
        self.file_object = f"<file: {self.filename}>"
    
    def close(self):
        print(f"close: Closing {self.filename}")
        self.file_object = None
    
    def __del__(self):
        print(f"__del__: Destroying {self.filename}")
        if self.file_object:
            self.close()

# Create and use
handler = FileHandler("data.txt")
handler.open()
handler.close()

# Delete explicitly
del handler
# Output:
# __init__: Initializing with data.txt
# open: Opening data.txt
# close: Closing data.txt
# __del__: Destroying data.txt
```

## Practical Examples

### Bank Account

```python
class BankAccount:
    def __init__(self, holder, initial_balance=0):
        self.holder = holder
        self.balance = initial_balance
        self.transactions = []
        self._log_transaction("OPEN", initial_balance)
    
    def deposit(self, amount):
        if amount <= 0:
            raise ValueError("Deposit amount must be positive")
        self.balance += amount
        self._log_transaction("DEPOSIT", amount)
        return self.balance
    
    def withdraw(self, amount):
        if amount <= 0:
            raise ValueError("Withdrawal amount must be positive")
        if amount > self.balance:
            raise ValueError("Insufficient funds")
        self.balance -= amount
        self._log_transaction("WITHDRAWAL", amount)
        return self.balance
    
    def _log_transaction(self, transaction_type, amount):
        self.transactions.append({
            "type": transaction_type,
            "amount": amount,
            "balance": self.balance
        })
    
    def get_balance(self):
        return self.balance
    
    def get_statement(self):
        print(f"Account Statement for {self.holder}")
        print("-" * 50)
        for txn in self.transactions:
            print(f"{txn['type']:10} ${txn['amount']:7.2f}  Balance: ${txn['balance']:7.2f}")

# Usage
account = BankAccount("Alice", 1000)
account.deposit(500)
account.withdraw(200)
account.get_statement()

print(f"\nCurrent Balance: ${account.get_balance():.2f}")
```

### Todo List

```python
class TodoItem:
    def __init__(self, title, description=""):
        self.title = title
        self.description = description
        self.completed = False
    
    def mark_complete(self):
        self.completed = True
    
    def mark_incomplete(self):
        self.completed = False
    
    def __str__(self):
        status = "✓" if self.completed else "☐"
        return f"{status} {self.title}"

class TodoList:
    def __init__(self):
        self.items = []
    
    def add_item(self, title, description=""):
        item = TodoItem(title, description)
        self.items.append(item)
        return item
    
    def remove_item(self, index):
        if 0 <= index < len(self.items):
            self.items.pop(index)
    
    def get_pending(self):
        return [item for item in self.items if not item.completed]
    
    def get_completed(self):
        return [item for item in self.items if item.completed]
    
    def display(self):
        print("Todo List:")
        for i, item in enumerate(self.items):
            print(f"{i}. {item}")

# Usage
todo_list = TodoList()
todo_list.add_item("Learn Python", "Master OOP")
todo_list.add_item("Build a project", "Create something useful")
todo_list.add_item("Read documentation", "Understand the ecosystem")

todo_list.items[0].mark_complete()
todo_list.display()

print(f"\nPending: {len(todo_list.get_pending())}")
print(f"Completed: {len(todo_list.get_completed())}")
```

## Common Mistakes

### Mistake 1: Forgetting self

```python
# WRONG - missing self parameter
class Dog:
    def bark(self):  # This is correct!
        return "Woof!"

# Can also be this:
class Cat:
    def meow(self):  # self is conventional name
        return "Meow"

# But using other names works too:
class Bird:
    def sing(bird):  # Works but not conventional!
        return "Tweet"

# Using it correctly
dog = Dog()
print(dog.bark())  # Output: Woof!
```

### Mistake 2: Mutable Default Arguments

```python
# WRONG - default list is shared!
class Container:
    def __init__(self, items=[]):
        self.items = items

c1 = Container()
c1.items.append("a")

c2 = Container()
print(c2.items)  # Output: ['a'] - UNEXPECTED!

# CORRECT - use None and create new list
class SafeContainer:
    def __init__(self, items=None):
        self.items = items if items is not None else []

c3 = SafeContainer()
c3.items.append("x")

c4 = SafeContainer()
print(c4.items)  # Output: [] - Correct!
```

### Mistake 3: Modifying Shared Class Attributes

```python
# WRONG - modifying class list affects all instances
class Config:
    settings = []
    
    def add_setting(self, setting):
        self.settings.append(setting)  # Modifies class attribute!

c1 = Config()
c1.add_setting("debug=true")

c2 = Config()
print(c2.settings)  # Output: ['debug=true'] - All instances affected!

# CORRECT - use instance attributes
class GoodConfig:
    def __init__(self):
        self.settings = []
    
    def add_setting(self, setting):
        self.settings.append(setting)

c3 = GoodConfig()
c3.add_setting("debug=true")

c4 = GoodConfig()
print(c4.settings)  # Output: [] - Correct!
```

### Mistake 4: Using Type Checks Instead of Duck Typing

```python
# WRONG - type checking (not Pythonic)
class Processor:
    def process(self, obj):
        if type(obj) == list:
            return sum(obj)
        elif type(obj) == str:
            return len(obj)

# CORRECT - use duck typing
class BetterProcessor:
    def process(self, obj):
        try:
            return sum(obj)  # Works with any sumerable
        except TypeError:
            return len(obj)  # Fall back to length
```

## Best Practices

### 1. Use Type Hints

```python
from typing import Optional, List

class Employee:
    def __init__(self, name: str, salary: float, manager: Optional['Employee'] = None):
        self.name = name
        self.salary = salary
        self.manager = manager
    
    def get_team(self) -> List[str]:
        return [self.name]
```

### 2. Document with Docstrings

```python
class DataProcessor:
    """Process and transform data.
    
    This class handles reading, transforming, and writing data.
    """
    
    def __init__(self, source: str):
        """Initialize processor.
        
        Args:
            source: Path to data source
        """
        self.source = source
    
    def process(self, data: dict) -> dict:
        """Process input data.
        
        Args:
            data: Input dictionary
            
        Returns:
            Processed dictionary
            
        Raises:
            ValueError: If data is invalid
        """
        if not data:
            raise ValueError("Data cannot be empty")
        return data
```

### 3. Use Properties for Encapsulation

```python
class Circle:
    def __init__(self, radius: float):
        if radius <= 0:
            raise ValueError("Radius must be positive")
        self._radius = radius
    
    @property
    def radius(self) -> float:
        return self._radius
    
    @radius.setter
    def radius(self, value: float) -> None:
        if value <= 0:
            raise ValueError("Radius must be positive")
        self._radius = value
    
    @property
    def area(self) -> float:
        return 3.14159 * self._radius ** 2
```

## Summary

| Concept | Description | Example |
|---------|-------------|---------|
| **Class** | Blueprint for objects | `class Dog:` |
| **Instance** | Object created from class | `dog = Dog()` |
| **Attribute** | Data stored in object | `self.name = "Buddy"` |
| **Method** | Function in object | `def bark(self):` |
| **Constructor** | Initializes object | `def __init__(self):` |
| **self** | Reference to instance | Used in all methods |
| **Class Method** | Operates on class | `@classmethod` |
| **Static Method** | No instance/class data | `@staticmethod` |
| **Property** | Getter/setter | `@property` |

### Key Takeaways

1. **Classes organize code** - Bundle data and behavior together
2. **self refers to instance** - Used to access instance data and methods
3. **__init__ initializes** - Called when object is created
4. **Methods operate on data** - Instance methods use self
5. **Attributes store state** - Both instance and class attributes available
6. **Special methods enable customization** - __str__, __add__, etc.
7. **Properties provide encapsulation** - Control access to attributes

### Practice Exercises

1. Create a Student class with GPA calculation
2. Implement a Book class with ISBN tracking
3. Build a Counter class that tracks object creation
4. Create a Rectangle class with area and perimeter methods
5. Implement a TemperatureConverter with Celsius/Fahrenheit properties

---

**Next:** Learn about inheritance to extend and reuse classes, then explore polymorphism and other OOP patterns.
