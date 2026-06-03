# Data Structures in Python

## Overview

Data structures are the fundamental building blocks for storing and organizing data in Python. This section covers the core data structures that every Python programmer should master.

## What You'll Learn

### Core Data Structures

1. **Tuples** - Immutable sequences for fixed data
   - Creating and using tuples
   - Immutability benefits
   - Namedtuples for structured data
   - Using tuples as dictionary keys

2. **Dictionaries** - Key-value mappings for flexible data
   - Creating and accessing dictionaries
   - Dictionary methods and operations
   - Nested dictionaries
   - Dictionary comprehensions
   - Common use cases (configuration, caching, JSON)

3. **Sets** - Unordered unique collections
   - Creating and managing sets
   - Set operations (union, intersection, difference)
   - Mathematical set operations
   - Frozensets for immutable sets

4. **Strings** - Text sequences with powerful methods
   - String creation and manipulation
   - String methods and formatting
   - F-strings for modern formatting
   - Regular expressions for pattern matching
   - Text processing techniques

## Data Structures Comparison

| Feature | List | Tuple | Set | Dict |
|---------|------|-------|-----|------|
| **Ordered** | Yes | Yes | No | Yes (3.7+) |
| **Mutable** | Yes | No | Yes | Yes |
| **Unique** | No | No | Yes (unique keys) | N/A |
| **Hashable** | No | Yes | No | No |
| **Access by Index** | Yes | Yes | No | By key |
| **Use Cases** | Dynamic collections | Fixed data, keys | Deduplication | Mappings |

## Quick Reference

### Creating Collections

```python
# List - ordered, mutable
my_list = [1, 2, 3]

# Tuple - ordered, immutable
my_tuple = (1, 2, 3)

# Set - unordered, unique, mutable
my_set = {1, 2, 3}

# Dictionary - key-value pairs
my_dict = {"key": "value", "a": 1}

# Empty collections
empty_list = []
empty_tuple = ()
empty_set = set()  # NOT {}!
empty_dict = {}
```

### Common Operations

```python
# Access
my_list[0]      # Index access
my_dict["key"]  # Key access
my_tuple[1]     # Index access

# Modification
my_list.append(4)           # Add to list
my_dict["new"] = "data"     # Add to dict
my_set.add(4)               # Add to set
# my_tuple.append(4)        # ERROR - immutable

# Iteration
for item in my_list: pass
for key, value in my_dict.items(): pass
for item in my_set: pass

# Check membership
2 in my_list        # True
"key" in my_dict    # True
2 in my_set         # True

# Length
len(my_list)
len(my_dict)
len(my_set)
```

## Performance Characteristics

### Time Complexity (Average Case)

| Operation | List | Tuple | Set | Dict |
|-----------|------|-------|-----|------|
| **Index access** | O(1) | O(1) | N/A | N/A |
| **Insert/Delete** | O(n) | N/A | O(1) | O(1) |
| **Search** | O(n) | O(n) | O(1) | O(1) |
| **Iteration** | O(n) | O(n) | O(n) | O(n) |

### Memory Usage

- **Tuples**: Most efficient, immutable overhead is minimal
- **Lists**: More overhead for dynamically resizable structure
- **Sets**: More memory per item due to hashing infrastructure
- **Dictionaries**: Most memory usage due to key-value storage and hashing

## Choosing the Right Data Structure

### Use Lists When:
- You need ordered, mutable collections
- You perform frequent modifications
- Index access is important
- Example: Task queue, shopping cart

### Use Tuples When:
- Data should not change (immutability required)
- You need hashable objects for dictionary keys or sets
- Returning multiple values from functions
- Example: Database records, coordinates, namedtuples

### Use Sets When:
- You need unique elements
- Membership testing must be fast
- You need set operations (union, intersection)
- Example: Deduplication, tags, permissions

### Use Dictionaries When:
- You need key-value mappings
- Keys are meaningful labels, not indices
- Flexible data structure needed
- Example: Configuration, user profiles, JSON data

## Common Patterns

### Deduplication

```python
# Remove duplicates (loses order)
items = [1, 2, 2, 3, 1, 4]
unique = list(set(items))

# Remove duplicates (preserves order)
seen = set()
unique = []
for item in items:
    if item not in seen:
        unique.append(item)
        seen.add(item)
```

### Grouping Data

```python
# Group by category
from collections import defaultdict
data = [("fruit", "apple"), ("fruit", "banana"), ("veg", "carrot")]
grouped = defaultdict(list)
for category, item in data:
    grouped[category].append(item)
```

### Finding Common Elements

```python
# Intersection of multiple lists
list1 = [1, 2, 3, 4, 5]
list2 = [3, 4, 5, 6, 7]
list3 = [5, 6, 7, 8, 9]

common = set(list1) & set(list2) & set(list3)
print(common)  # {5}
```

### Counting Occurrences

```python
from collections import Counter

data = ["apple", "banana", "apple", "cherry", "banana", "apple"]
counter = Counter(data)
print(counter.most_common(2))  # [('apple', 3), ('banana', 2)]
```

## Advanced Topics

### Collections Module

Python's `collections` module provides specialized data structures:

- **namedtuple**: Named tuple subclass for structured data
- **deque**: Double-ended queue for efficient appends/pops
- **Counter**: Dictionary subclass for counting objects
- **OrderedDict**: Dictionary that preserves insertion order (Python 3.7+ regular dicts are ordered)
- **defaultdict**: Dictionary with default factory function

Example:

```python
from collections import namedtuple, Counter, defaultdict

# Named tuple
Point = namedtuple('Point', ['x', 'y'])
p = Point(10, 20)

# Counter
words = ['hello', 'world', 'hello']
freq = Counter(words)

# Default dict
graph = defaultdict(list)
graph['a'].append('b')
```

### Type Hints for Data Structures

Python 3.5+ supports type hints for clarity:

```python
from typing import List, Tuple, Set, Dict, Optional

def process_data(
    items: List[str],
    coords: Tuple[int, int],
    unique: Set[str],
    config: Dict[str, int]
) -> Optional[List[str]]:
    return items
```

## Best Practices

1. **Choose the right structure** - Match the structure to the problem
2. **Use type hints** - Document expected types
3. **Leverage built-in methods** - They're optimized and tested
4. **Understand performance** - Know O(1) vs O(n) operations
5. **Consider immutability** - Use tuples for thread safety
6. **Document assumptions** - Comment on expected data structure

## Practice Exercises

1. **Inventory System**: Create a system to track products (name, quantity, price) using dictionaries
2. **Word Analyzer**: Find the most common words in a text using Counter
3. **Duplicate Finder**: Write a function to find duplicates across multiple lists using sets
4. **Data Transformer**: Convert data between list, tuple, set, and dictionary formats
5. **Performance Comparison**: Time different data structure operations to understand performance

## Resources

- [Official Python Docs - Data Structures](https://docs.python.org/3/tutorial/datastructures.html)
- [Collections Module](https://docs.python.org/3/library/collections.html)
- [Built-in Types](https://docs.python.org/3/library/stdtypes.html)

## Next Steps

- Explore **Object-Oriented Programming** to create custom data structures
- Learn **Functional Programming** for advanced data manipulation
- Study **File Handling** to persist data structures to disk
- Investigate **Performance Optimization** for large datasets

---

**Module Status**: All core data structures covered. Ready for advanced topics.
