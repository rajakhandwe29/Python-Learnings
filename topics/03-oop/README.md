# Object-Oriented Programming (OOP) in Python

## Overview

Object-Oriented Programming is a paradigm that organizes code around objects and their interactions. Python is an excellent language for learning and practicing OOP principles.

## What You'll Learn

### Core OOP Concepts

1. **Classes and Objects** - The foundation of OOP
   - Creating classes and instances
   - Attributes and methods
   - Constructors and initialization
   - Special methods for customization

2. **Inheritance** - Extending and reusing code
   - Single and multiple inheritance
   - Method overriding
   - Super function for parent access
   - Method Resolution Order (MRO)

3. **Polymorphism** - Objects taking multiple forms
   - Duck typing
   - Method overriding
   - Operator overloading
   - Polymorphic collections

4. **Encapsulation** - Protecting object state
   - Public, protected, private access levels
   - Properties and getters/setters
   - Data validation
   - Name mangling

5. **Design Patterns** - Proven solutions to common problems
   - Creational patterns (Singleton, Factory, Builder)
   - Structural patterns (Adapter, Decorator, Proxy)
   - Behavioral patterns (Observer, Strategy, State)

## SOLID Principles

### Single Responsibility Principle (SRP)
A class should have only one reason to change:

```python
# BAD - multiple responsibilities
class User:
    def save_to_database(self): pass
    def send_email(self): pass
    def generate_report(self): pass

# GOOD - single responsibility
class User:
    def __init__(self, name, email): pass

class UserRepository:
    def save(self, user): pass

class EmailService:
    def send(self, user, message): pass
```

### Open/Closed Principle (OCP)
Open for extension, closed for modification:

```python
# BAD - must modify to add shapes
def calculate_area(shapes):
    total = 0
    for shape in shapes:
        if isinstance(shape, Circle):
            total += 3.14 * shape.radius ** 2
        elif isinstance(shape, Square):
            total += shape.side ** 2

# GOOD - extends without modifying
class Shape:
    def area(self): pass

class Circle(Shape):
    def area(self):
        return 3.14 * self.radius ** 2

class Square(Shape):
    def area(self):
        return self.side ** 2

def calculate_area(shapes):
    return sum(shape.area() for shape in shapes)
```

### Liskov Substitution Principle (LSP)
Derived classes must be substitutable for base classes:

```python
# CORRECT - Penguin can't fly, so don't inherit from Bird
class Bird:
    def move(self): pass

class FlyingBird(Bird):
    def fly(self): pass

class Penguin(Bird):
    def swim(self): pass
```

### Interface Segregation Principle (ISP)
Clients shouldn't depend on interfaces they don't use:

```python
# BAD - large interface
class Worker:
    def work(self): pass
    def eat(self): pass

# GOOD - segregated interfaces
class Workable:
    def work(self): pass

class Eatable:
    def eat(self): pass

class Human(Workable, Eatable):
    def work(self): pass
    def eat(self): pass

class Robot(Workable):
    def work(self): pass
```

### Dependency Inversion Principle (DIP)
Depend on abstractions, not concretions:

```python
# BAD - depends on concrete class
class Car:
    def __init__(self):
        self.engine = DieselEngine()

# GOOD - depends on abstraction
class Car:
    def __init__(self, engine):
        self.engine = engine  # Could be any engine type
```

## Class Hierarchy Example

```python
# Base class
class Vehicle:
    def __init__(self, make, model):
        self.make = make
        self.model = model
    
    def start(self):
        raise NotImplementedError

# Derived class
class Car(Vehicle):
    def __init__(self, make, model, num_doors):
        super().__init__(make, model)
        self.num_doors = num_doors
    
    def start(self):
        return f"{self.make} {self.model} started"

# Another derived class
class Motorcycle(Vehicle):
    def __init__(self, make, model, cc):
        super().__init__(make, model)
        self.cc = cc
    
    def start(self):
        return f"{self.make} {self.model} ({self.cc}cc) started"

# Usage
vehicles = [
    Car("Toyota", "Camry", 4),
    Motorcycle("Harley", "Street 750", 750),
    Car("Honda", "Civic", 4)
]

for vehicle in vehicles:
    print(vehicle.start())
```

## When to Use OOP

### Good for:
- Complex systems with multiple entities
- Systems requiring extensibility
- Modeling real-world problems
- Large team projects
- Applications with clear hierarchies

### Not necessary for:
- Simple scripts
- Data transformation pipelines
- Functional algorithms
- Quick one-off programs

## Common OOP Mistakes

### 1. Over-Engineering
Using OOP for problems better solved with functions or data structures.

### 2. Massive Classes
Classes that do too much (God Object anti-pattern).

### 3. Deep Inheritance Hierarchies
Hard to understand and maintain.

### 4. Ignoring Composition
Composition is often better than inheritance.

### 5. Breaking Encapsulation
Accessing private attributes directly.

## Best Practices Summary

1. **Keep classes focused** - Single responsibility
2. **Use composition over inheritance** - More flexible
3. **Prefer public interfaces** - Make intentional contracts
4. **Use type hints** - Document expected types
5. **Write docstrings** - Document behavior
6. **Test thoroughly** - Especially inheritance
7. **Refactor regularly** - Improve design over time
8. **Follow SOLID principles** - Write maintainable code

## Project Structure

```
myproject/
├── models/
│   ├── __init__.py
│   ├── user.py
│   ├── product.py
│   └── order.py
├── services/
│   ├── __init__.py
│   ├── user_service.py
│   └── payment_service.py
├── repositories/
│   ├── __init__.py
│   └── user_repository.py
└── main.py
```

## Testing OOP Code

```python
import unittest

class TestUser(unittest.TestCase):
    def setUp(self):
        self.user = User("Alice", "alice@example.com")
    
    def test_user_creation(self):
        self.assertEqual(self.user.name, "Alice")
        self.assertEqual(self.user.email, "alice@example.com")
    
    def test_invalid_email(self):
        with self.assertRaises(ValueError):
            User("Bob", "invalid-email")
```

## Resources

- [Official Python OOP Tutorial](https://docs.python.org/3/tutorial/classes.html)
- [SOLID Principles](https://en.wikipedia.org/wiki/SOLID)
- [Design Patterns](https://refactoring.guru/design-patterns)
- [Clean Code](https://www.oreilly.com/library/view/clean-code-a/9780136083238/)

## Next Steps

- **Functional Programming**: Explore lambda, map, filter, reduce
- **File Handling**: Learn to read/write data
- **Error Handling**: Master exception handling
- **Modules and Packages**: Organize code into reusable units
- **Advanced Topics**: Threading, async programming, testing

## Module Structure

- **Classes and Objects**: Foundation concepts (7500+ words)
- **Inheritance**: Code reuse through hierarchies (5500+ words)
- **Polymorphism**: Multiple forms and dynamic dispatch (5700+ words)
- **Encapsulation**: Protecting object state (5600+ words)
- **Design Patterns**: Common solutions (4500+ words)

---

**Total Module**: Comprehensive OOP knowledge covering all essential concepts and patterns.

Ready to explore **Functional Programming** for a different programming paradigm!
