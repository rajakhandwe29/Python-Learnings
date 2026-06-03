# Encapsulation in Python: A Comprehensive Guide

## Table of Contents
1. [Introduction](#introduction)
2. [Access Modifiers](#access-modifiers)
3. [Private Attributes](#private-attributes)
4. [Protected Attributes](#protected-attributes)
5. [Properties and Getters/Setters](#properties-and-getterssetters)
6. [Data Validation](#data-validation)
7. [Name Mangling](#name-mangling)
8. [Practical Examples](#practical-examples)
9. [Common Mistakes](#common-mistakes)
10. [Best Practices](#best-practices)
11. [Summary](#summary)

## Introduction

Encapsulation is the bundling of data (attributes) and methods that operate on that data within a single unit (class), while hiding the internal details. It's about controlling access to an object's internals and maintaining invariants.

### Why Encapsulation Matters

Encapsulation provides:
- Data protection from unauthorized access
- Implementation hiding (internals don't matter to users)
- Controlled access through interfaces
- Easier maintenance and refactoring
- Prevents accidental misuse

### Quick Example

```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance  # Private attribute
    
    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount
    
    def withdraw(self, amount):
        if 0 < amount <= self.__balance:
            self.__balance -= amount
    
    def get_balance(self):
        return self.__balance

account = BankAccount(1000)
account.deposit(500)
print(account.get_balance())  # Output: 1500
# account.__balance = -5000  # Can't do this directly!
```

## Access Modifiers

### Public Attributes

```python
class Person:
    def __init__(self, name):
        self.name = name  # Public attribute

person = Person("Alice")
print(person.name)  # Can access directly
person.name = "Bob"  # Can modify directly
print(person.name)  # Output: Bob
```

### Protected Attributes (Convention)

```python
class BankAccount:
    def __init__(self, balance):
        self._balance = balance  # Protected by convention (single underscore)
    
    def get_balance(self):
        return self._balance
    
    def set_balance(self, amount):
        if amount >= 0:
            self._balance = amount

account = BankAccount(1000)
print(account._balance)  # Accessible but not recommended

# Should use methods instead
print(account.get_balance())  # Output: 1000
account.set_balance(1500)
print(account.get_balance())  # Output: 1500

# The underscore signals "don't use this directly"
# But Python still allows it (it's a convention, not enforcement)
```

### Private Attributes

```python
class SecureAccount:
    def __init__(self, balance):
        self.__balance = balance  # Private (double underscore)
    
    def get_balance(self):
        return self.__balance
    
    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount

account = SecureAccount(1000)
print(account.get_balance())  # Output: 1000

# Cannot access __balance directly
# print(account.__balance)  # AttributeError

# Name mangling makes it private
print(account._SecureAccount__balance)  # Output: 1000 (but don't do this!)
```

## Private Attributes

### Benefits of Private Attributes

```python
class Stack:
    def __init__(self):
        self.__items = []  # Private - users can't access directly
    
    def push(self, item):
        self.__items.append(item)
    
    def pop(self):
        if len(self.__items) == 0:
            raise ValueError("Stack is empty")
        return self.__items.pop()
    
    def is_empty(self):
        return len(self.__items) == 0
    
    def size(self):
        return len(self.__items)

stack = Stack()
stack.push(1)
stack.push(2)
stack.push(3)

print(stack.pop())  # Output: 3
print(stack.size())  # Output: 2

# Can't do this:
# stack.__items.clear()  # Would break the stack invariant

# Can only use proper interface:
stack.pop()
stack.pop()
print(stack.is_empty())  # Output: True
```

### Ensuring Invariants

```python
class Temperature:
    def __init__(self, celsius):
        self.__celsius = None
        self.celsius = celsius  # Use setter for validation
    
    @property
    def celsius(self):
        return self.__celsius
    
    @celsius.setter
    def celsius(self, value):
        if value < -273.15:
            raise ValueError("Temperature cannot be below absolute zero")
        self.__celsius = value
    
    @property
    def fahrenheit(self):
        return self.__celsius * 9/5 + 32

# Guaranteed to maintain invariant
temp = Temperature(25)
print(f"{temp.celsius}°C = {temp.fahrenheit:.1f}°F")
# Output: 25°C = 77.0°F

try:
    temp.celsius = -300  # Violates invariant
except ValueError as e:
    print(f"Error: {e}")  # Output: Error: Temperature cannot be below absolute zero
```

## Protected Attributes

### Single Underscore Convention

```python
class Logger:
    def __init__(self, name):
        self._name = name  # Protected - subclasses can use
        self._level = "INFO"
    
    def _log(self, message):
        """Internal method - not part of public API"""
        print(f"[{self._level}] {self._name}: {message}")
    
    def info(self, message):
        self._log(message)

class FileLogger(Logger):
    def __init__(self, name, filename):
        super().__init__(name)
        self._filename = filename  # Protected attribute
    
    def _log(self, message):
        # Can access parent's protected attributes
        with open(self._filename, 'a') as f:
            f.write(f"[{self._level}] {self._name}: {message}\n")

logger = Logger("myapp")
logger.info("App started")

# Users know not to use _log directly
# But subclasses can extend it
```

## Properties and Getters/Setters

### Using @property Decorator

```python
class Rectangle:
    def __init__(self, width, height):
        self._width = width
        self._height = height
    
    @property
    def width(self):
        """Get width"""
        return self._width
    
    @width.setter
    def width(self, value):
        """Set width with validation"""
        if value <= 0:
            raise ValueError("Width must be positive")
        self._width = value
    
    @property
    def area(self):
        """Calculated property - read-only"""
        return self._width * self._height

rect = Rectangle(10, 5)

# Use properties like attributes
print(rect.width)   # Output: 10
print(rect.area)    # Output: 50

# Set with validation
rect.width = 15
print(rect.area)    # Output: 75

# Trying to set invalid value
try:
    rect.width = -5
except ValueError as e:
    print(f"Error: {e}")
```

### Lazy Evaluation

```python
class ExpensiveObject:
    def __init__(self):
        self._data = None
    
    @property
    def data(self):
        """Load data only when accessed"""
        if self._data is None:
            print("Loading expensive data...")
            self._data = self._load_data()
        return self._data
    
    def _load_data(self):
        """Expensive operation"""
        import time
        time.sleep(1)  # Simulate expensive operation
        return "Important Data"

obj = ExpensiveObject()
print("Object created")
print(obj.data)  # First access loads data
print(obj.data)  # Second access uses cached data
```

## Data Validation

### Validation in Setters

```python
class User:
    def __init__(self, username, email, age):
        self._username = None
        self._email = None
        self._age = None
        
        # Use setters for validation
        self.username = username
        self.email = email
        self.age = age
    
    @property
    def username(self):
        return self._username
    
    @username.setter
    def username(self, value):
        if not value or len(value) < 3:
            raise ValueError("Username must be at least 3 characters")
        self._username = value
    
    @property
    def email(self):
        return self._email
    
    @email.setter
    def email(self, value):
        if "@" not in value:
            raise ValueError("Invalid email format")
        self._email = value
    
    @property
    def age(self):
        return self._age
    
    @age.setter
    def age(self, value):
        if not isinstance(value, int) or value < 0 or value > 150:
            raise ValueError("Age must be between 0 and 150")
        self._age = value

# Valid creation
user = User("alice_wonder", "alice@example.com", 25)
print(f"{user.username}: {user.email} ({user.age} years)")

# Invalid attempts
try:
    user.username = "ab"
except ValueError as e:
    print(f"Error: {e}")

try:
    user.email = "invalid"
except ValueError as e:
    print(f"Error: {e}")

try:
    user.age = 200
except ValueError as e:
    print(f"Error: {e}")
```

## Name Mangling

### Double Underscore Behavior

```python
class Parent:
    def __init__(self):
        self.__private = "Parent private"
        self._protected = "Parent protected"
        self.public = "Parent public"

class Child(Parent):
    def __init__(self):
        super().__init__()
        self.__private = "Child private"  # Different from parent's!
    
    def show(self):
        print(f"Child private: {self.__private}")
        print(f"Protected: {self._protected}")
        print(f"Public: {self.public}")

child = Child()
child.show()
# Output:
# Child private: Child private
# Protected: Parent protected
# Public: Parent public

# Name mangling creates unique names
print(dir(child))  # Shows _Child__private and _Parent__private
```

### When to Use Name Mangling

```python
# Use double underscore for:
# 1. Really private implementation details
# 2. Avoiding name conflicts in inheritance

class Base:
    def __init__(self):
        self.__config = {}  # True private
    
    def _get_config(self):
        """Protected - for subclass use"""
        return self.__config

class Derived(Base):
    def __init__(self):
        super().__init__()
        self.__config = {}  # Different from parent - no conflict!
    
    def setup(self):
        base_config = self._get_config()
        print(f"Base config: {base_config}")
        print(f"My config: {self.__config}")

d = Derived()
d.setup()
```

## Practical Examples

### Bank Account System

```python
class BankAccount:
    def __init__(self, holder, initial_balance=0):
        self.__holder = holder
        self.__balance = initial_balance
        self.__transactions = []
        self.__lock_account = False
    
    @property
    def balance(self):
        return self.__balance
    
    @property
    def holder(self):
        return self.__holder
    
    def deposit(self, amount):
        if self.__lock_account:
            raise ValueError("Account is locked")
        if amount <= 0:
            raise ValueError("Deposit amount must be positive")
        
        self.__balance += amount
        self.__transactions.append(("deposit", amount))
        return self.__balance
    
    def withdraw(self, amount):
        if self.__lock_account:
            raise ValueError("Account is locked")
        if amount <= 0:
            raise ValueError("Withdrawal amount must be positive")
        if amount > self.__balance:
            raise ValueError("Insufficient funds")
        
        self.__balance -= amount
        self.__transactions.append(("withdraw", amount))
        return self.__balance
    
    def lock(self):
        self.__lock_account = True
    
    def unlock(self):
        self.__lock_account = False
    
    def get_statement(self):
        print(f"\nStatement for {self.__holder}")
        print("-" * 40)
        for txn_type, amount in self.__transactions:
            print(f"{txn_type.capitalize():10} ${amount:7.2f}")
        print(f"{'Balance':10} ${self.__balance:7.2f}")

# Usage
account = BankAccount("John Doe", 1000)
account.deposit(500)
account.withdraw(200)
print(f"Balance: ${account.balance}")

account.get_statement()

account.lock()
try:
    account.withdraw(100)
except ValueError as e:
    print(f"Error: {e}")
```

### Configuration Manager

```python
class Config:
    def __init__(self):
        self.__settings = {}
        self.__defaults = {
            "debug": False,
            "timeout": 30,
            "max_retries": 3
        }
    
    def _init_defaults(self):
        """Protected method to initialize defaults"""
        self.__settings = self.__defaults.copy()
    
    def get(self, key, default=None):
        """Get configuration value"""
        return self.__settings.get(key, default)
    
    def set(self, key, value):
        """Set configuration value with validation"""
        if key == "timeout":
            if not isinstance(value, int) or value <= 0:
                raise ValueError("Timeout must be positive integer")
        elif key == "max_retries":
            if not isinstance(value, int) or value < 0:
                raise ValueError("Max retries cannot be negative")
        
        self.__settings[key] = value
    
    def reset_to_defaults(self):
        """Reset to default configuration"""
        self.__settings = self.__defaults.copy()
    
    def to_dict(self):
        """Get all settings (read-only copy)"""
        return self.__settings.copy()

config = Config()
config._init_defaults()

print(config.get("debug"))     # Output: False
config.set("debug", True)
print(config.get("debug"))     # Output: True

try:
    config.set("timeout", -10)
except ValueError as e:
    print(f"Error: {e}")

print(config.to_dict())
```

## Common Mistakes

### Mistake 1: Over-Encapsulation

```python
# WRONG - too many getters/setters for simple data
class Point:
    def __init__(self, x, y):
        self.__x = x
        self.__y = y
    
    @property
    def x(self):
        return self.__x
    
    @x.setter
    def x(self, value):
        self.__x = value
    
    @property
    def y(self):
        return self.__y
    
    @y.setter
    def y(self, value):
        self.__y = value

# CORRECT - keep it simple
class SimplePoint:
    def __init__(self, x, y):
        self.x = x  # Public is fine for simple data
        self.y = y
```

### Mistake 2: Encapsulation Without Interface

```python
# WRONG - private but no way to use it
class DataProcessor:
    def __init__(self, data):
        self.__data = data
    
    # No way to get the processed data!

# CORRECT - provide necessary interface
class GoodDataProcessor:
    def __init__(self, data):
        self.__data = data
    
    def process(self):
        # Process the data
        return self.__data

    def get_result(self):
        return self.__data
```

### Mistake 3: Trusting in Name Mangling for Security

```python
# WRONG - relying on name mangling for security
class SecurePassword:
    def __init__(self, password):
        self.__password = password

obj = SecurePassword("secret123")
# Someone can still access it:
print(obj._SecurePassword__password)  # Output: secret123

# CORRECT - name mangling is for avoiding conflicts, not security
# For real security, use proper libraries like hashlib
import hashlib

class ProperPassword:
    def __init__(self, password):
        self.__password_hash = hashlib.sha256(password.encode()).hexdigest()
    
    def verify(self, password):
        return hashlib.sha256(password.encode()).hexdigest() == self.__password_hash
```

## Best Practices

### 1. Start Public, Make Private Only When Needed

```python
# GOOD - simple attributes stay public
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

# Only make private when you need validation or control
class Temperature:
    def __init__(self, celsius):
        self._celsius = celsius
    
    @property
    def celsius(self):
        return self._celsius
    
    @celsius.setter
    def celsius(self, value):
        if value < -273.15:
            raise ValueError("Invalid temperature")
        self._celsius = value
```

### 2. Use Properties for Attribute Access

```python
# GOOD - property looks like attribute but provides control
class Person:
    def __init__(self, name):
        self._name = name
    
    @property
    def name(self):
        return self._name
    
    @name.setter
    def name(self, value):
        if not value:
            raise ValueError("Name cannot be empty")
        self._name = value

person = Person("Alice")
print(person.name)  # Looks like attribute
person.name = "Bob"  # Can validate in setter
```

### 3. Document Protected Members

```python
class DataStore:
    def __init__(self):
        self._cache = {}  # Protected cache for subclasses
    
    def get(self, key):
        if key not in self._cache:
            self._cache[key] = self._load(key)
        return self._cache[key]
    
    def _load(self, key):
        """Protected method for subclass override"""
        raise NotImplementedError
```

## Summary

| Level | Syntax | Access | Use For |
|-------|--------|--------|---------|
| **Public** | `name` | Anywhere | Public API |
| **Protected** | `_name` | Subclasses | Implementation details |
| **Private** | `__name` | Only inside class | Avoid name conflicts |

### Key Takeaways

1. **Encapsulation protects invariants** - ensure valid state
2. **Use properties for controlled access** - validation in setters
3. **Protected (_) is convention** - subclasses can use it
4. **Private (__) has name mangling** - avoid conflicts in inheritance
5. **Start public, make private if needed** - YAGNI principle
6. **Document the interface** - tell users what's available
7. **Use validation in setters** - maintain object invariants

### Practice Exercises

1. Create a BankAccount class with balance validation
2. Implement a User class with email validation
3. Build a Configuration class with type checking
4. Create a Stack class with private item storage
5. Implement a Cache class with automatic expiration

---

**Next:** Explore design patterns to solve common programming problems elegantly.
