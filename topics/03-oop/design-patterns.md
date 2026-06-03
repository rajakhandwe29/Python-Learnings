# Design Patterns in Python: A Comprehensive Guide

## Table of Contents
1. [Introduction](#introduction)
2. [Creational Patterns](#creational-patterns)
3. [Structural Patterns](#structural-patterns)
4. [Behavioral Patterns](#behavioral-patterns)
5. [Common Patterns Summary](#common-patterns-summary)
6. [When to Use Each Pattern](#when-to-use-each-pattern)
7. [Anti-Patterns](#anti-patterns)
8. [Best Practices](#best-practices)
9. [Summary](#summary)

## Introduction

Design patterns are reusable solutions to common programming problems. They provide tested, proven templates for writing reliable code. This guide covers the most important patterns for Python developers.

### Categories of Design Patterns

- **Creational**: Object creation mechanisms
- **Structural**: Object composition and relationships
- **Behavioral**: Object collaboration and responsibility distribution

## Creational Patterns

### Singleton Pattern

```python
class Database:
    _instance = None
    
    def __new__(cls):
        if cls._instance is None:
            cls._instance = super().__new__(cls)
            cls._instance.connection = "Connected to DB"
        return cls._instance

# Always returns same instance
db1 = Database()
db2 = Database()
print(db1 is db2)  # Output: True
print(db1.connection)  # Output: Connected to DB
```

### Factory Pattern

```python
class Document:
    def create(self):
        pass

class PDFDocument(Document):
    def create(self):
        return "Creating PDF"

class ExcelDocument(Document):
    def create(self):
        return "Creating Excel"

class DocumentFactory:
    @staticmethod
    def create_document(doc_type):
        if doc_type == "pdf":
            return PDFDocument()
        elif doc_type == "excel":
            return ExcelDocument()
        raise ValueError(f"Unknown type: {doc_type}")

# Usage
factory = DocumentFactory()
pdf = factory.create_document("pdf")
excel = factory.create_document("excel")

print(pdf.create())    # Output: Creating PDF
print(excel.create())  # Output: Creating Excel
```

### Builder Pattern

```python
class DatabaseConfig:
    def __init__(self):
        self.host = None
        self.port = None
        self.database = None
        self.user = None
        self.password = None
    
    def __repr__(self):
        return f"DB({self.host}:{self.port}/{self.database})"

class DatabaseConfigBuilder:
    def __init__(self):
        self.config = DatabaseConfig()
    
    def set_host(self, host):
        self.config.host = host
        return self
    
    def set_port(self, port):
        self.config.port = port
        return self
    
    def set_database(self, database):
        self.config.database = database
        return self
    
    def set_user(self, user):
        self.config.user = user
        return self
    
    def set_password(self, password):
        self.config.password = password
        return self
    
    def build(self):
        return self.config

# Usage - Method chaining
config = (DatabaseConfigBuilder()
    .set_host("localhost")
    .set_port(5432)
    .set_database("myapp")
    .set_user("admin")
    .set_password("secret")
    .build())

print(config)  # Output: DB(localhost:5432/myapp)
```

## Structural Patterns

### Adapter Pattern

```python
# Old interface
class LegacyPaymentProcessor:
    def process_payment(self, amount):
        print(f"Legacy: Processing ${amount}")

# New interface expected
class NewPaymentProcessor:
    def execute_transaction(self, amount):
        print(f"New: Executing ${amount} transaction")

# Adapter to make old interface work with new system
class PaymentAdapter:
    def __init__(self, legacy_processor):
        self.legacy = legacy_processor
    
    def execute_transaction(self, amount):
        self.legacy.process_payment(amount)

# Usage
legacy = LegacyPaymentProcessor()
adapter = PaymentAdapter(legacy)
adapter.execute_transaction(100)  # Output: Legacy: Processing $100
```

### Decorator Pattern

```python
import time

def log_execution(func):
    def wrapper(*args, **kwargs):
        print(f"Executing {func.__name__}")
        start = time.time()
        result = func(*args, **kwargs)
        elapsed = time.time() - start
        print(f"Completed in {elapsed:.4f}s")
        return result
    return wrapper

@log_execution
def slow_function(n):
    time.sleep(0.1)
    return n * 2

result = slow_function(5)
print(f"Result: {result}")
# Output:
# Executing slow_function
# Completed in 0.1009s
# Result: 10
```

### Proxy Pattern

```python
class RealDatabase:
    def query(self, sql):
        print(f"Executing: {sql}")
        return "Result"

class DatabaseProxy:
    def __init__(self):
        self._real_db = None
        self._cache = {}
    
    def query(self, sql):
        # Check cache first
        if sql in self._cache:
            print(f"Cache hit for: {sql}")
            return self._cache[sql]
        
        # Lazy initialization
        if self._real_db is None:
            self._real_db = RealDatabase()
        
        result = self._real_db.query(sql)
        self._cache[sql] = result
        return result

# Usage
db = DatabaseProxy()
db.query("SELECT * FROM users")
db.query("SELECT * FROM users")  # Cache hit
```

## Behavioral Patterns

### Observer Pattern

```python
class Subject:
    def __init__(self):
        self._observers = []
    
    def attach(self, observer):
        self._observers.append(observer)
    
    def detach(self, observer):
        self._observers.remove(observer)
    
    def notify(self, message):
        for observer in self._observers:
            observer.update(message)

class Observer:
    def __init__(self, name):
        self.name = name
    
    def update(self, message):
        print(f"{self.name} received: {message}")

# Usage
subject = Subject()
observer1 = Observer("Observer1")
observer2 = Observer("Observer2")

subject.attach(observer1)
subject.attach(observer2)

subject.notify("Event occurred!")
# Output:
# Observer1 received: Event occurred!
# Observer2 received: Event occurred!
```

### Strategy Pattern

```python
from abc import ABC, abstractmethod

class SortingStrategy(ABC):
    @abstractmethod
    def sort(self, data):
        pass

class BubbleSort(SortingStrategy):
    def sort(self, data):
        print("Sorting with Bubble Sort")
        return sorted(data)

class QuickSort(SortingStrategy):
    def sort(self, data):
        print("Sorting with Quick Sort")
        return sorted(data)

class DataProcessor:
    def __init__(self, strategy):
        self.strategy = strategy
    
    def process(self, data):
        return self.strategy.sort(data)

# Usage
data = [3, 1, 4, 1, 5, 9, 2, 6]

processor = DataProcessor(BubbleSort())
result1 = processor.process(data)

processor = DataProcessor(QuickSort())
result2 = processor.process(data)
```

### State Pattern

```python
from abc import ABC, abstractmethod

class State(ABC):
    @abstractmethod
    def handle(self, context):
        pass

class SimpleState(State):
    def handle(self, context):
        print("In Simple State")
        context.state = ComplexState()

class ComplexState(State):
    def handle(self, context):
        print("In Complex State")
        context.state = SimpleState()

class Context:
    def __init__(self):
        self.state = SimpleState()
    
    def request(self):
        self.state.handle(self)

# Usage
context = Context()
context.request()  # Output: In Simple State
context.request()  # Output: In Complex State
context.request()  # Output: In Simple State
```

### Command Pattern

```python
from abc import ABC, abstractmethod

class Command(ABC):
    @abstractmethod
    def execute(self):
        pass

class LightOnCommand(Command):
    def __init__(self, light):
        self.light = light
    
    def execute(self):
        self.light.turn_on()

class LightOffCommand(Command):
    def __init__(self, light):
        self.light = light
    
    def execute(self):
        self.light.turn_off()

class Light:
    def turn_on(self):
        print("Light is on")
    
    def turn_off(self):
        print("Light is off")

class RemoteControl:
    def __init__(self):
        self.commands = {}
    
    def set_command(self, slot, command):
        self.commands[slot] = command
    
    def press_button(self, slot):
        if slot in self.commands:
            self.commands[slot].execute()

# Usage
light = Light()
remote = RemoteControl()

remote.set_command("on", LightOnCommand(light))
remote.set_command("off", LightOffCommand(light))

remote.press_button("on")   # Output: Light is on
remote.press_button("off")  # Output: Light is off
```

## Common Patterns Summary

| Pattern | Purpose | Use Case |
|---------|---------|----------|
| **Singleton** | Single instance | Database connection, logger |
| **Factory** | Create objects | Different types of objects |
| **Builder** | Complex construction | Configuration objects |
| **Adapter** | Interface compatibility | Legacy code integration |
| **Decorator** | Add functionality | Logging, caching, timing |
| **Proxy** | Control access | Lazy loading, access control |
| **Observer** | Notify multiple objects | Event handling, MVC |
| **Strategy** | Interchange algorithms | Different implementations |
| **State** | Behavior based on state | State machines |
| **Command** | Encapsulate requests | Undo/redo, macros |

## When to Use Each Pattern

### Singleton
- Database connections
- Logger instances
- Configuration objects
- Thread pools

### Factory
- Creating objects without knowing exact classes
- Centralizing object creation
- Supporting multiple product families

### Builder
- Complex objects with many optional parameters
- Step-by-step construction
- Immutable objects

### Observer
- Event-driven systems
- MVC architectures
- Publish-subscribe patterns

### Strategy
- Multiple algorithms for same task
- Runtime algorithm selection
- Avoiding conditional statements

## Anti-Patterns

### God Object (Antipattern)

```python
# BAD - class does everything
class BadClass:
    def load_data(self): pass
    def save_data(self): pass
    def process_data(self): pass
    def send_email(self): pass
    def generate_report(self): pass

# GOOD - separate concerns
class DataLoader:
    def load_data(self): pass

class DataProcessor:
    def process_data(self): pass

class EmailSender:
    def send_email(self): pass
```

### Spaghetti Code (Antipattern)

```python
# BAD - complex nested logic
def process():
    if x:
        if y:
            if z:
                do_something()

# GOOD - clear flow
def process():
    if not conditions_met():
        return
    do_something()

def conditions_met():
    return x and y and z
```

## Best Practices

### 1. Avoid Over-Engineering

```python
# WRONG - unnecessary pattern
class SimpleValue:
    _instance = None
    def __new__(cls):
        if not cls._instance:
            cls._instance = super().__new__(cls)
        return cls._instance

# CORRECT - simple class
class SimpleValue:
    pass
```

### 2. Choose Patterns Based on Requirements

```python
# Don't use patterns just because you know them
# Use them to solve actual problems

# If you need one instance of something:
class Logger:
    _instance = None
    @classmethod
    def getInstance(cls):
        if not cls._instance:
            cls._instance = Logger()
        return cls._instance

# If you just need shared functionality:
class Logger:
    def log(self, message):
        print(message)

logger = Logger()  # Simple and effective
```

### 3. Keep Patterns Simple

```python
# GOOD - straightforward implementation
class Factory:
    @staticmethod
    def create(type_name):
        if type_name == "A":
            return ClassA()
        elif type_name == "B":
            return ClassB()

# Avoid over-complicated pattern implementations
```

## Summary

| Category | Patterns | Purpose |
|----------|----------|---------|
| **Creational** | Singleton, Factory, Builder | Object creation |
| **Structural** | Adapter, Decorator, Proxy | Object composition |
| **Behavioral** | Observer, Strategy, State, Command | Object interaction |

### Key Takeaways

1. **Know your patterns** - but don't overuse them
2. **Solve problems, not complexity** - patterns are tools
3. **Keep it simple** - simple code beats clever code
4. **Use when needed** - don't force patterns on code
5. **Documentation matters** - explain why you used a pattern
6. **Refactor toward patterns** - emerge from code
7. **Learn from frameworks** - Django, Flask use patterns

### Practice Exercises

1. Implement Singleton for application configuration
2. Create Factory for different data store types
3. Build Observer for event notification system
4. Implement Strategy for different payment methods
5. Create State pattern for order workflow

---

**Next:** Master functional programming for data transformation and elegant code.
