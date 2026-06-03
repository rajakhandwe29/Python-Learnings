# Generators in Python: A Comprehensive Guide

## Introduction

Generators are functions that yield values one at a time, allowing lazy evaluation and memory-efficient iteration. They produce values on-demand rather than computing everything upfront.

## Basic Generators

```python
def simple_generator():
    yield 1
    yield 2
    yield 3

# Create generator object
gen = simple_generator()
print(next(gen))  # Output: 1
print(next(gen))  # Output: 2
print(next(gen))  # Output: 3
# next(gen)  # StopIteration exception

# Iterate generator
for value in simple_generator():
    print(value)
# Output:
# 1
# 2
# 3
```

## Generator Functions

```python
# Traditional approach - store all in memory
def range_list(n):
    result = []
    for i in range(n):
        result.append(i)
    return result

# Generator approach - compute on demand
def range_generator(n):
    i = 0
    while i < n:
        yield i
        i += 1

# Memory efficient
gen = range_generator(1000000)
print(next(gen))  # Only computes first value
print(next(gen))  # Computes second value
# Rest not computed unless accessed
```

## Generator Expressions

```python
# Similar to list comprehension but with ()
squares_list = [x**2 for x in range(5)]
squares_gen = (x**2 for x in range(5))

print(list(squares_list))  # [0, 1, 4, 9, 16]
print(list(squares_gen))   # [0, 1, 4, 9, 16]

# Generator is memory-efficient
import sys
print(sys.getsizeof(squares_list))  # ~104 bytes
print(sys.getsizeof(squares_gen))   # ~128 bytes (but only stores current value)
```

## Generator with send()

```python
def echo_generator():
    while True:
        value = yield
        if value is not None:
            print(f"Received: {value}")

gen = echo_generator()
next(gen)  # Prime generator

gen.send(10)  # Output: Received: 10
gen.send("hello")  # Output: Received: hello
```

## Generator with throw()

```python
def safe_generator():
    try:
        yield 1
        yield 2
        yield 3
    except ValueError:
        print("Caught ValueError")
        yield "error_handled"

gen = safe_generator()
print(next(gen))        # Output: 1
print(next(gen))        # Output: 2
print(gen.throw(ValueError))  # Output: Caught ValueError / error_handled
```

## Practical Examples

### File Reading
```python
def read_file_by_line(filename):
    with open(filename) as f:
        for line in f:
            yield line.strip()

# Process large files efficiently
for line in read_file_by_line("large_file.txt"):
    print(line)
    # Only one line in memory at a time
```

### Fibonacci Sequence
```python
def fibonacci():
    a, b = 0, 1
    while True:
        yield a
        a, b = b, a + b

# Get first 10 Fibonacci numbers
fib = fibonacci()
fib_sequence = [next(fib) for _ in range(10)]
print(fib_sequence)  # [0, 1, 1, 2, 3, 5, 8, 13, 21, 34]
```

### Infinite Sequence
```python
def infinite_counter(start=0):
    count = start
    while True:
        yield count
        count += 1

# Use itertools.islice to get limited values
import itertools
counter = itertools.islice(infinite_counter(), 5)
print(list(counter))  # [0, 1, 2, 3, 4]
```

### Data Processing Pipeline
```python
def read_numbers(filename):
    with open(filename) as f:
        for line in f:
            yield int(line.strip())

def filter_even(numbers):
    for num in numbers:
        if num % 2 == 0:
            yield num

def multiply_by_two(numbers):
    for num in numbers:
        yield num * 2

# Chain generators for efficient pipeline
result = multiply_by_two(filter_even(read_numbers("numbers.txt")))
for value in result:
    print(value)
```

## Best Practices

### 1. Use Generators for Large Datasets
```python
# GOOD - memory efficient
def process_large_file(filename):
    with open(filename) as f:
        for line in f:
            yield process_line(line)

# BAD - loads entire file in memory
def process_large_file_bad(filename):
    with open(filename) as f:
        return [process_line(line) for line in f]
```

### 2. Generator Expressions Over List Comprehensions (When Appropriate)
```python
# GOOD - if not using all values
squares = (x**2 for x in range(1000000))
print(next(squares))  # Only computes first

# LESS GOOD - if need all values
squares = [x**2 for x in range(1000000)]
```

### 3. Close Generators When Done
```python
def resource_generator():
    resource = open("file.txt")
    try:
        for line in resource:
            yield line
    finally:
        resource.close()

gen = resource_generator()
# Make sure to close if not iterating fully
gen.close()
```

## Summary

| Feature | Generator | List |
|---------|-----------|------|
| **Memory** | Lazy - on demand | Eager - all upfront |
| **Speed** | Fast initially | Slow for large data |
| **Syntax** | `yield` | `[ ]` |
| **Reusable** | No - exhausted after iteration | Yes - can iterate multiple times |

### Key Takeaways

1. **Generators are lazy** - compute on demand
2. **Memory efficient** - don't store all values
3. **Use yield** - special keyword for generators
4. **One-time use** - exhaust after iteration
5. **Perfect for streaming** - large files, APIs
6. **Chain generators** - build data pipelines
7. **Consider itertools** - module for advanced generators

---

**Next:** Create a comprehensive functional programming summary and move to file handling!
