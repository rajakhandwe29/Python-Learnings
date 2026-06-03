# Functional Programming in Python

## Overview

Functional programming is a paradigm emphasizing immutability, pure functions, and function composition. Python supports functional programming concepts alongside its imperative and OOP capabilities.

## What You'll Learn

### Core Concepts

1. **Lambda Functions** - Anonymous functions for short operations
   - Simple lambda syntax
   - Using with map, filter, sorted
   - Closures and function factories

2. **Map, Filter, Reduce** - Higher-order functions
   - Transforming data with map
   - Filtering with conditions
   - Aggregating with reduce

3. **Decorators** - Function modification and enhancement
   - Basic decorators
   - Factory patterns
   - Common decorators (logging, timing, caching)

4. **Generators** - Lazy evaluation and memory efficiency
   - Generator functions with yield
   - Generator expressions
   - Infinite sequences and pipelines

## Functional vs Imperative

```python
# Imperative - HOW to do it
numbers = [1, 2, 3, 4, 5]
squared = []
for num in numbers:
    if num % 2 == 0:
        squared.append(num ** 2)

# Functional - WHAT to do
squares = [x**2 for x in numbers if x % 2 == 0]

# Functional with map/filter
squares = list(map(lambda x: x**2, filter(lambda x: x % 2 == 0, numbers)))
```

## Pure Functions

```python
# Pure function - same input always gives same output, no side effects
def add(a, b):
    return a + b

# Impure function - has side effects
counter = 0
def add_impure(a, b):
    global counter
    counter += 1  # Side effect!
    print(f"Called {counter} times")  # Side effect!
    return a + b
```

## Immutability

```python
# Immutable approach
data = (1, 2, 3)
new_data = data + (4,)  # Creates new tuple

# Mutable approach (not functional)
data = [1, 2, 3]
data.append(4)  # Modifies original list
```

## Function Composition

```python
# Composing functions
def compose(*functions):
    def composed(arg):
        for f in reversed(functions):
            arg = f(arg)
        return arg
    return composed

def add_one(x):
    return x + 1

def double(x):
    return x * 2

# compose(double, add_one)(5) -> double(add_one(5)) -> double(6) -> 12
pipeline = compose(double, add_one)
print(pipeline(5))  # Output: 12
```

## Common Patterns

### map() - Transform Data
```python
numbers = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x**2, numbers))
# Or better:
squared = [x**2 for x in numbers]
```

### filter() - Select Data
```python
numbers = [1, 2, 3, 4, 5, 6]
evens = list(filter(lambda x: x % 2 == 0, numbers))
# Or better:
evens = [x for x in numbers if x % 2 == 0]
```

### reduce() - Aggregate Data
```python
from functools import reduce
numbers = [1, 2, 3, 4, 5]
total = reduce(lambda x, y: x + y, numbers)
# Or better:
total = sum(numbers)
```

## Functional Programming Tools

### itertools Module
```python
import itertools

# Infinite counter
counter = itertools.count(1)
print(next(counter))  # 1
print(next(counter))  # 2

# Chain iterables
combined = itertools.chain([1, 2], [3, 4], [5, 6])
print(list(combined))  # [1, 2, 3, 4, 5, 6]

# Combination and permutation
pairs = itertools.combinations([1, 2, 3], 2)
print(list(pairs))  # [(1, 2), (1, 3), (2, 3)]
```

### functools Module
```python
import functools

# reduce
result = functools.reduce(lambda x, y: x + y, [1, 2, 3, 4])
print(result)  # 10

# partial - fix arguments
multiply_by_two = functools.partial(lambda x, y: x * y, 2)
print(multiply_by_two(5))  # 10

# lru_cache - memoization
@functools.lru_cache(maxsize=128)
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n-1) + fibonacci(n-2)

print(fibonacci(30))  # Fast due to caching
```

## Best Practices

1. **Prefer comprehensions** - More Pythonic than map/filter
2. **Use pure functions** - Easier to test and reason about
3. **Avoid side effects** - Don't modify state or globals
4. **Compose functions** - Build complex behavior from simple parts
5. **Use appropriate tools** - map/filter for transformations, generators for iteration
6. **Document higher-order functions** - Explain what decorators and functions do
7. **Consider readability** - Functional doesn't always mean better

## When to Use Functional Programming

### Good For:
- Data transformation pipelines
- Parallel processing (immutability helps)
- Mathematical operations
- Lazy evaluation requirements

### Less Suitable For:
- Complex state management
- Stateful operations
- User interfaces
- Real-world modeling

## Comparison with OOP

```python
# OOP approach
class Student:
    def __init__(self, name, grades):
        self.name = name
        self.grades = grades
    
    def average(self):
        return sum(self.grades) / len(self.grades)

# Functional approach
student = {"name": "Alice", "grades": [85, 90, 88]}
average = lambda s: sum(s["grades"]) / len(s["grades"])
print(average(student))  # 87.67

# Mixed approach (Pythonic)
students = [
    {"name": "Alice", "grades": [85, 90, 88]},
    {"name": "Bob", "grades": [92, 88, 95]}
]

averages = [
    (s["name"], sum(s["grades"]) / len(s["grades"]))
    for s in students
]
```

## Key Concepts Review

| Concept | Description | Example |
|---------|-------------|---------|
| **Lambda** | Anonymous function | `lambda x: x * 2` |
| **Map** | Transform each element | `map(func, iterable)` |
| **Filter** | Select matching elements | `filter(func, iterable)` |
| **Reduce** | Combine to single value | `reduce(func, iterable)` |
| **Decorator** | Wrap function behavior | `@decorator` |
| **Generator** | Lazy evaluation | `yield value` |
| **Pure Function** | No side effects | `def add(a, b): return a + b` |
| **Composition** | Combine functions | `f(g(h(x)))` |

## Resources

- [Python functools documentation](https://docs.python.org/3/library/functools.html)
- [Python itertools documentation](https://docs.python.org/3/library/itertools.html)
- [PEP 289 - Generators](https://www.python.org/dev/peps/pep-0289/)

## Next Steps

- **File Handling** - Read and write data
- **Error Handling** - Handle exceptions gracefully
- **Modules and Packages** - Organize code
- **Advanced Topics** - Threading, async, testing

---

**Total Module**: Functional programming concepts with practical Python examples.
