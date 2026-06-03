# Map, Filter, and Reduce in Python

## Introduction

These three higher-order functions are cornerstones of functional programming. They operate on iterables and enable powerful data transformations.

## Map Function

```python
# map(function, iterable) applies function to each element

numbers = [1, 2, 3, 4, 5]

# Double each number
doubled = list(map(lambda x: x * 2, numbers))
print(doubled)  # Output: [2, 4, 6, 8, 10]

# Convert to strings
as_strings = list(map(str, numbers))
print(as_strings)  # Output: ['1', '2', '3', '4', '5']

# With custom function
def square(x):
    return x ** 2

squared = list(map(square, numbers))
print(squared)  # Output: [1, 4, 9, 16, 25]

# Multiple iterables
list1 = [1, 2, 3]
list2 = [4, 5, 6]

sums = list(map(lambda x, y: x + y, list1, list2))
print(sums)  # Output: [5, 7, 9]
```

## Filter Function

```python
# filter(function, iterable) keeps elements where function returns True

numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Get even numbers
evens = list(filter(lambda x: x % 2 == 0, numbers))
print(evens)  # Output: [2, 4, 6, 8, 10]

# Get numbers greater than 5
greater_than_5 = list(filter(lambda x: x > 5, numbers))
print(greater_than_5)  # Output: [6, 7, 8, 9, 10]

# Filter with None (removes falsy values)
mixed = [0, 1, False, 2, '', 'hello', [], [1, 2, 3]]
truthy = list(filter(None, mixed))
print(truthy)  # Output: [1, 2, 'hello', [1, 2, 3]]

# With custom function
def is_long_word(word):
    return len(word) > 3

words = ['cat', 'dogs', 'python', 'a', 'programming']
long_words = list(filter(is_long_word, words))
print(long_words)  # Output: ['dogs', 'python', 'programming']
```

## Reduce Function

```python
from functools import reduce

# reduce(function, iterable) combines elements into single value

numbers = [1, 2, 3, 4, 5]

# Sum
total = reduce(lambda x, y: x + y, numbers)
print(total)  # Output: 15

# Product
product = reduce(lambda x, y: x * y, numbers)
print(product)  # Output: 120

# Concatenate strings
words = ['hello', ' ', 'world']
sentence = reduce(lambda x, y: x + y, words)
print(sentence)  # Output: 'hello world'

# Find maximum
maximum = reduce(lambda x, y: x if x > y else y, numbers)
print(maximum)  # Output: 5

# With initial value
result = reduce(lambda x, y: x + y, numbers, 10)  # Start with 10
print(result)  # Output: 25 (10 + 15)
```

## Practical Examples

### Data Transformation Pipeline
```python
data = [
    {"name": "Alice", "age": 30, "salary": 50000},
    {"name": "Bob", "age": 25, "salary": 40000},
    {"name": "Charlie", "age": 35, "salary": 60000}
]

# Filter (age > 25), Map (get names), Reduce (join)
result = reduce(
    lambda x, y: f"{x}, {y}",
    map(
        lambda person: person["name"],
        filter(lambda person: person["age"] > 25, data)
    )
)

print(result)  # Output: Alice, Charlie
```

### Working with Collections
```python
students = [
    {"name": "Alice", "scores": [85, 90, 88]},
    {"name": "Bob", "scores": [92, 88, 95]},
    {"name": "Charlie", "scores": [78, 80, 82]}
]

# Get average for each student
averages = list(map(
    lambda s: (s["name"], sum(s["scores"]) / len(s["scores"])),
    students
))

print(averages)
# Output: [('Alice', 87.66...), ('Bob', 91.66...), ('Charlie', 80.0)]
```

## Best Practices

### Use Comprehensions When Possible
```python
# Good for simple operations - more Pythonic
squared = [x ** 2 for x in numbers]

# Less Pythonic
squared = list(map(lambda x: x ** 2, numbers))
```

### Keep Lambdas Simple
```python
# GOOD - clear intent
squared = list(map(lambda x: x ** 2, numbers))

# BAD - too complex
result = list(map(
    lambda x: (x ** 2) + (3 * x) if x > 0 else (x ** 2) - (3 * x),
    numbers
))

# BETTER
def complex_calculation(x):
    base = x ** 2
    adjustment = 3 * x if x > 0 else -3 * x
    return base + adjustment

result = list(map(complex_calculation, numbers))
```

### Chain Operations Carefully
```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Readable pipeline
result = (
    numbers
    |> filter(lambda x: x % 2 == 0)      # Evens
    |> map(lambda x: x ** 2)              # Square them
    |> filter(lambda x: x > 20)           # Greater than 20
)

# But Python doesn't have pipe operator, so use comprehensions instead:
result = [
    x ** 2
    for x in numbers
    if x % 2 == 0 and x ** 2 > 20
]

print(result)  # Output: [36, 64, 100]
```

## Summary

| Function | Purpose | Returns |
|----------|---------|---------|
| **map** | Transform each element | Iterator |
| **filter** | Keep matching elements | Iterator |
| **reduce** | Combine to single value | Single value |

### Comparison with Comprehensions

```python
# map - transformation
mapped = list(map(lambda x: x * 2, [1, 2, 3]))
comp = [x * 2 for x in [1, 2, 3]]

# filter - selection
filtered = list(filter(lambda x: x > 2, [1, 2, 3]))
comp = [x for x in [1, 2, 3] if x > 2]

# reduce - aggregation
from functools import reduce
reduced = reduce(lambda x, y: x + y, [1, 2, 3])
comp = sum([1, 2, 3])
```

### Key Takeaways

1. **map transforms** - applies function to each element
2. **filter selects** - keeps elements matching condition
3. **reduce aggregates** - combines to single value
4. **List comprehensions are more Pythonic** - prefer for simple cases
5. **Reduce is less commonly used** - explicit loops are clearer
6. **Combine for power** - chain operations for complex transformations
7. **Remember generators** - map and filter return iterators

---

**Next:** Learn decorators to wrap and extend function behavior!
