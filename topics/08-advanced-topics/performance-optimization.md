# Performance Optimization

## Profiling

```python
import cProfile
import pstats

def fibonacci(n):
    if n < 2:
        return n
    return fibonacci(n-1) + fibonacci(n-2)

# Profile function
profiler = cProfile.Profile()
profiler.enable()
fibonacci(30)
profiler.disable()

stats = pstats.Stats(profiler)
stats.sort_stats("cumulative")
stats.print_stats()
```

## Time Optimization

```python
import timeit

# Original
def slow_sum(n):
    total = 0
    for i in range(n):
        total += i
    return total

# Optimized
def fast_sum(n):
    return n * (n - 1) // 2

# Compare
t1 = timeit.timeit(lambda: slow_sum(10000), number=10000)
t2 = timeit.timeit(lambda: fast_sum(10000), number=10000)
print(f"Slow: {t1}, Fast: {t2}")
```

## Caching

```python
from functools import lru_cache

@lru_cache(maxsize=128)
def fibonacci(n):
    if n < 2:
        return n
    return fibonacci(n-1) + fibonacci(n-2)

print(fibonacci(100))  # Fast with cache
```

## Memory Optimization

```python
# Generator (memory efficient)
def large_list_generator():
    for i in range(1000000):
        yield i

# Use generator instead of list
for item in large_list_generator():
    process(item)

# Avoid storing large lists
# WRONG: data = [process_item(i) for i in range(1000000)]
# RIGHT: data = (process_item(i) for i in range(1000000))
```

## Common Optimizations

```python
# List comprehension vs loop
# Faster: [x*2 for x in range(1000)]
# Slower: result = []; [result.append(x*2) for x in range(1000)]

# String concatenation
# WRONG: s = ""; s += "a"; s += "b"
# RIGHT: s = "".join(["a", "b"])

# Lookup optimization
# Use sets for membership
s = {1, 2, 3}  # O(1) lookup
if 2 in s: ...
```

## Best Practices

1. **Profile before optimizing** - Find bottlenecks
2. **Use caching** - Avoid repeated work
3. **Generators for large data** - Memory efficient
4. **List comprehensions** - Faster than loops
5. **Algorithm matters** - O(n) vs O(n²)

---

Complete your Python journey!
