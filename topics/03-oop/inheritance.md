# Inheritance in Python: A Comprehensive Guide

## Table of Contents
1. [Introduction](#introduction)
2. [Basic Inheritance](#basic-inheritance)
3. [Method Overriding](#method-overriding)
4. [Super Function](#super-function)
5. [Multiple Inheritance](#multiple-inheritance)
6. [Method Resolution Order](#method-resolution-order)
7. [Abstract Base Classes](#abstract-base-classes)
8. [Practical Examples](#practical-examples)
9. [Common Mistakes](#common-mistakes)
10. [Best Practices](#best-practices)
11. [Summary](#summary)

## Introduction

Inheritance is a core OOP principle that allows a class (child/derived class) to inherit properties and methods from another class (parent/base class). This enables code reuse and logical hierarchies.

### Why Inheritance Matters

Inheritance provides:
- Code reusability
- Hierarchical organization
- Polymorphic behavior
- Extensibility
- DRY (Don't Repeat Yourself) principle

### Quick Example

```python
# Parent class
class Animal:
    def __init__(self, name):
        self.name = name
    
    def speak(self):
        return f"{self.name} makes a sound"

# Child class inherits from Animal
class Dog(Animal):
    def speak(self):
        return f"{self.name} says: Woof!"

# Usage
dog = Dog("Buddy")
print(dog.speak())  # Output: Buddy says: Woof!
print(dog.name)     # Output: Buddy
```

## Basic Inheritance

### Single Inheritance

```python
class Vehicle:
    def __init__(self, make, model):
        self.make = make
        self.model = model
    
    def get_info(self):
        return f"{self.make} {self.model}"

class Car(Vehicle):
    def __init__(self, make, model, num_doors):
        super().__init__(make, model)  # Call parent constructor
        self.num_doors = num_doors
    
    def get_info(self):
        parent_info = super().get_info()
        return f"{parent_info} ({self.num_doors} doors)"

# Usage
car = Car("Toyota", "Camry", 4)
print(car.get_info())  # Output: Toyota Camry (4 doors)
print(car.make)        # Output: Toyota
print(car.model)       # Output: Camry
```

### Inheriting Attributes and Methods

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def introduce(self):
        return f"Hi, I'm {self.name} and I'm {self.age} years old"
    
    def birthday(self):
        self.age += 1
        return f"{self.name} is now {self.age} years old"

class Student(Person):
    def __init__(self, name, age, grade):
        super().__init__(name, age)
        self.grade = grade
    
    def study(self):
        return f"{self.name} is studying"

# Usage
student = Student("Alice", 20, "A")
print(student.introduce())  # Output: Hi, I'm Alice and I'm 20 years old
print(student.study())      # Output: Alice is studying
print(student.birthday())   # Output: Alice is now 21 years old
```

### Checking Inheritance

```python
class Animal:
    pass

class Dog(Animal):
    pass

dog = Dog()

# Check instance type
print(type(dog))            # Output: <class '__main__.Dog'>

# Check if instance of class
print(isinstance(dog, Dog))     # Output: True
print(isinstance(dog, Animal))  # Output: True

# Check if subclass
print(issubclass(Dog, Animal))   # Output: True
print(issubclass(Animal, Dog))   # Output: False

# Get MRO (Method Resolution Order)
print(Dog.__mro__)  # Output: (<class 'Dog'>, <class 'Animal'>, <class 'object'>)
```

## Method Overriding

### Overriding Methods

```python
class Shape:
    def area(self):
        return 0
    
    def perimeter(self):
        return 0

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height
    
    def area(self):
        return self.width * self.height
    
    def perimeter(self):
        return 2 * (self.width + self.height)

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius
    
    def area(self):
        return 3.14159 * self.radius ** 2
    
    def perimeter(self):
        return 2 * 3.14159 * self.radius

# Usage
rect = Rectangle(10, 5)
print(f"Rectangle area: {rect.area()}")           # Output: Rectangle area: 50
print(f"Rectangle perimeter: {rect.perimeter()}") # Output: Rectangle perimeter: 30

circle = Circle(5)
print(f"Circle area: {circle.area():.2f}")        # Output: Circle area: 78.54
print(f"Circle perimeter: {circle.perimeter():.2f}")  # Output: Circle perimeter: 31.42
```

### Adding New Methods

```python
class Employee:
    def __init__(self, name, salary):
        self.name = name
        self.salary = salary
    
    def work(self):
        return f"{self.name} is working"

class Manager(Employee):
    def __init__(self, name, salary, team_size):
        super().__init__(name, salary)
        self.team_size = team_size
    
    def manage(self):
        return f"{self.name} is managing a team of {self.team_size}"
    
    def conduct_meeting(self):
        return f"{self.name} is conducting a meeting"

# Usage
manager = Manager("Bob", 80000, 5)
print(manager.work())           # Output: Bob is working
print(manager.manage())         # Output: Bob is managing a team of 5
print(manager.conduct_meeting())  # Output: Bob is conducting a meeting
```

## Super Function

### Using super()

```python
class Parent:
    def __init__(self, name):
        self.name = name
    
    def display(self):
        return f"Name: {self.name}"

class Child(Parent):
    def __init__(self, name, age):
        super().__init__(name)  # Call parent constructor
        self.age = age
    
    def display(self):
        parent_display = super().display()  # Call parent method
        return f"{parent_display}, Age: {self.age}"

# Usage
child = Child("Charlie", 15)
print(child.display())  # Output: Name: Charlie, Age: 15
```

### super() with Arguments

```python
class A:
    def method(self):
        print("A's method")

class B(A):
    def method(self):
        print("B's method (before)")
        super().method()
        print("B's method (after)")

class C(A):
    def method(self):
        print("C's method (before)")
        super().method()
        print("C's method (after)")

class D(B, C):
    def method(self):
        print("D's method (before)")
        super().method()
        print("D's method (after)")

# Usage
d = D()
d.method()
# Output:
# D's method (before)
# B's method (before)
# C's method (before)
# A's method
# C's method (after)
# B's method (after)
# D's method (after)
```

## Multiple Inheritance

### Basic Multiple Inheritance

```python
class Walking:
    def walk(self):
        return "Walking..."

class Swimming:
    def swim(self):
        return "Swimming..."

class Running:
    def run(self):
        return "Running..."

class Athlete(Walking, Swimming, Running):
    def __init__(self, name):
        self.name = name
    
    def train(self):
        return f"{self.name} is training"

# Usage
athlete = Athlete("Alice")
print(athlete.walk())   # Output: Walking...
print(athlete.swim())   # Output: Swimming...
print(athlete.run())    # Output: Running...
print(athlete.train())  # Output: Alice is training
```

### Mixin Pattern

```python
class TimestampMixin:
    def get_timestamp(self):
        from datetime import datetime
        return datetime.now().isoformat()

class JournalEntry(TimestampMixin):
    def __init__(self, content):
        self.content = content
    
    def display(self):
        return f"[{self.get_timestamp()}] {self.content}"

class BlogPost(TimestampMixin):
    def __init__(self, title, body):
        self.title = title
        self.body = body
    
    def publish(self):
        return f"Published at {self.get_timestamp()}: {self.title}"

# Usage
entry = JournalEntry("Had a great day")
print(entry.display())

post = BlogPost("Python Tips", "Learn Python efficiently")
print(post.publish())
```

### Diamond Problem

```python
# The diamond problem - which parent's method is called?
class A:
    def method(self):
        return "A"

class B(A):
    def method(self):
        return "B -> " + super().method()

class C(A):
    def method(self):
        return "C -> " + super().method()

class D(B, C):
    pass

# Usage
d = D()
print(d.method())  # Output: B -> C -> A
# MRO: D -> B -> C -> A
print(D.__mro__)   # Shows method resolution order
```

## Method Resolution Order

### Understanding MRO

```python
class A:
    pass

class B(A):
    pass

class C(A):
    pass

class D(B, C):
    pass

# View method resolution order
print(D.__mro__)  
# Output: (<class 'D'>, <class 'B'>, <class 'C'>, <class 'A'>, <class 'object'>)

# Using mro() method
for cls in D.mro():
    print(cls.__name__)
# Output:
# D
# B
# C
# A
# object
```

## Abstract Base Classes

### Using ABC Module

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    """Abstract base class for shapes"""
    
    @abstractmethod
    def area(self):
        """Calculate area - must be implemented by subclasses"""
        pass
    
    @abstractmethod
    def perimeter(self):
        """Calculate perimeter - must be implemented by subclasses"""
        pass
    
    def description(self):
        """Concrete method - available to all subclasses"""
        return "This is a shape"

# Cannot instantiate abstract class
# shape = Shape()  # TypeError: Can't instantiate abstract class

class Square(Shape):
    def __init__(self, side):
        self.side = side
    
    def area(self):
        return self.side ** 2
    
    def perimeter(self):
        return 4 * self.side

# Can instantiate concrete class
square = Square(5)
print(f"Area: {square.area()}")          # Output: Area: 25
print(f"Perimeter: {square.perimeter()}") # Output: Perimeter: 20
print(square.description())              # Output: This is a shape
```

### Abstract Methods and Properties

```python
from abc import ABC, abstractmethod

class DataStore(ABC):
    @abstractmethod
    def save(self, data):
        pass
    
    @abstractmethod
    def load(self, key):
        pass
    
    @property
    @abstractmethod
    def is_connected(self):
        pass

class FileStore(DataStore):
    def __init__(self):
        self.connected = True
    
    def save(self, data):
        return f"Saving {data} to file"
    
    def load(self, key):
        return f"Loading {key} from file"
    
    @property
    def is_connected(self):
        return self.connected

# Usage
store = FileStore()
print(store.save("data"))  # Output: Saving data to file
print(store.load("key"))   # Output: Loading key from file
print(store.is_connected)  # Output: True
```

## Practical Examples

### Animal Hierarchy

```python
class Animal:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def speak(self):
        return "Some sound"
    
    def eat(self, food):
        return f"{self.name} is eating {food}"

class Mammal(Animal):
    def feed_young(self):
        return f"{self.name} is nursing young"

class Dog(Mammal):
    def __init__(self, name, age, breed):
        super().__init__(name, age)
        self.breed = breed
    
    def speak(self):
        return f"{self.name} says: Woof!"
    
    def fetch(self):
        return f"{self.name} is fetching the ball"

class Cat(Mammal):
    def speak(self):
        return f"{self.name} says: Meow"
    
    def scratch(self):
        return f"{self.name} is scratching"

# Usage
dog = Dog("Buddy", 3, "Golden Retriever")
print(dog.speak())        # Output: Buddy says: Woof!
print(dog.eat("kibble"))  # Output: Buddy is eating kibble
print(dog.fetch())        # Output: Buddy is fetching the ball
print(dog.feed_young())   # Output: Buddy is nursing young

cat = Cat("Whiskers", 5)
print(cat.speak())        # Output: Whiskers says: Meow
print(cat.scratch())      # Output: Whiskers is scratching
```

### Vehicle System

```python
from abc import ABC, abstractmethod

class Vehicle(ABC):
    def __init__(self, make, model):
        self.make = make
        self.model = model
        self.is_running = False
    
    @abstractmethod
    def start(self):
        pass
    
    @abstractmethod
    def stop(self):
        pass
    
    def get_info(self):
        return f"{self.make} {self.model}"

class Car(Vehicle):
    def __init__(self, make, model, num_doors):
        super().__init__(make, model)
        self.num_doors = num_doors
    
    def start(self):
        self.is_running = True
        return f"{self.get_info()} engine started"
    
    def stop(self):
        self.is_running = False
        return f"{self.get_info()} engine stopped"

class Motorcycle(Vehicle):
    def __init__(self, make, model, cc):
        super().__init__(make, model)
        self.cc = cc
    
    def start(self):
        self.is_running = True
        return f"{self.get_info()} engine started ({self.cc}cc)"
    
    def stop(self):
        self.is_running = False
        return f"{self.get_info()} engine stopped"

# Usage
car = Car("Toyota", "Camry", 4)
print(car.start())  # Output: Toyota Camry engine started
print(car.stop())   # Output: Toyota Camry engine stopped

bike = Motorcycle("Harley", "Street 750", 750)
print(bike.start()) # Output: Harley Street 750 engine started (750cc)
print(bike.stop())  # Output: Harley Street 750 engine stopped
```

## Common Mistakes

### Mistake 1: Forgetting to Call super().__init__()

```python
# WRONG - parent attributes not initialized
class Parent:
    def __init__(self, name):
        self.name = name

class Child(Parent):
    def __init__(self, name, age):
        # Forgot to call super().__init__()!
        self.age = age

child = Child("Alice", 10)
# print(child.name)  # AttributeError: 'Child' object has no attribute 'name'

# CORRECT - call parent constructor
class GoodChild(Parent):
    def __init__(self, name, age):
        super().__init__(name)
        self.age = age

good_child = GoodChild("Alice", 10)
print(good_child.name)  # Output: Alice
print(good_child.age)   # Output: 10
```

### Mistake 2: Modifying Parent Class Attributes

```python
# WRONG - modifying shared list
class Container:
    items = []  # Shared class attribute!

class SpecialContainer(Container):
    def add(self, item):
        self.items.append(item)

c1 = SpecialContainer()
c1.add("a")

c2 = SpecialContainer()
print(c2.items)  # Output: ['a'] - UNEXPECTED!

# CORRECT - use instance attributes
class GoodContainer:
    def __init__(self):
        self.items = []
    
    def add(self, item):
        self.items.append(item)

c3 = GoodContainer()
c3.add("x")

c4 = GoodContainer()
print(c4.items)  # Output: [] - Correct!
```

### Mistake 3: Breaking Liskov Substitution Principle

```python
# WRONG - derived class changes expected behavior
class Bird:
    def fly(self):
        return "Flying..."

class Penguin(Bird):
    def fly(self):
        raise NotImplementedError("Penguins can't fly!")

# This breaks LSP because Penguin can't be used where Bird is expected
def make_bird_fly(bird):
    return bird.fly()

# make_bird_fly(Penguin())  # Raises error!

# CORRECT - use proper inheritance hierarchy
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
        return "Penguin swimming..."
```

## Best Practices

### 1. Favor Composition Over Inheritance

```python
# GOOD - composition is more flexible
class Engine:
    def start(self):
        return "Engine started"

class Car:
    def __init__(self):
        self.engine = Engine()
    
    def start(self):
        return self.engine.start()

car = Car()
print(car.start())  # Output: Engine started

# LESS GOOD - inheritance creates tight coupling
class InheritedCar(Engine):
    pass
```

### 2. Use Abstract Base Classes

```python
from abc import ABC, abstractmethod

class DataProcessor(ABC):
    @abstractmethod
    def process(self, data):
        pass

class JSONProcessor(DataProcessor):
    def process(self, data):
        return f"Processing JSON: {data}"

class CSVProcessor(DataProcessor):
    def process(self, data):
        return f"Processing CSV: {data}"

# This enforces implementation in subclasses
```

### 3. Keep Inheritance Simple

```python
# GOOD - single level of inheritance
class Animal:
    pass

class Dog(Animal):
    pass

# LESS GOOD - deep inheritance hierarchy (hard to maintain)
class LivingThing:
    pass

class Organism(LivingThing):
    pass

class Animal(Organism):
    pass

class Mammal(Animal):
    pass

class Canine(Mammal):
    pass

class Dog(Canine):
    pass
```

## Summary

| Concept | Description | Example |
|---------|-------------|---------|
| **Inheritance** | Derive class from parent | `class Dog(Animal):` |
| **Override** | Replace parent method | `def speak(self): ...` |
| **Super** | Call parent method | `super().method()` |
| **MRO** | Method resolution order | `Class.__mro__` |
| **ABC** | Abstract base class | `class ABC(ABC): ...` |
| **Abstract Method** | Must be implemented | `@abstractmethod` |
| **Mixin** | Shared functionality | Multiple inheritance pattern |
| **Diamond Problem** | MRO ambiguity | Resolved by C3 linearization |

### Key Takeaways

1. **Inheritance enables code reuse** - Don't repeat code
2. **Override methods in subclasses** - Customize behavior
3. **Use super() to access parent** - Don't hardcode parent class name
4. **Understand MRO** - Know method resolution order
5. **Use ABC for contracts** - Ensure subclass implementation
6. **Favor composition** - More flexible than deep inheritance
7. **Keep hierarchy shallow** - Easier to understand and maintain

### Practice Exercises

1. Create an employee hierarchy with different job types
2. Build a vehicle system with various vehicle types
3. Implement a shape inheritance tree with area calculations
4. Create a plugin system using abstract base classes
5. Design a payment processor hierarchy for different payment methods

---

**Next:** Explore polymorphism to understand runtime behavior differences and dynamic method dispatch.
