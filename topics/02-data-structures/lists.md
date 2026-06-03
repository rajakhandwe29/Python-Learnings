# Lists

Master Python's most versatile data structure.

## What is a List?

An ordered, mutable collection that can store multiple items.

```python
# Creating lists
empty_list = []
numbers = [1, 2, 3, 4, 5]
mixed = [1, "text", 3.14, True, None]
nested = [[1, 2], [3, 4], [5, 6]]

print(type(numbers))  # <class 'list'>
```

---

## Accessing Elements

### Indexing

```python
fruits = ["apple", "banana", "orange", "grape", "mango"]

# Positive indexing (left to right)
print(fruits[0])    # apple (first)
print(fruits[2])    # orange (third)
print(fruits[-1])   # mango (last)
print(fruits[-2])   # grape (second from last)

# Index out of range error
# print(fruits[10])  # ❌ IndexError
```

### Slicing

```python
fruits = ["apple", "banana", "orange", "grape", "mango"]

# Slicing [start:end:step]
print(fruits[1:4])      # ['banana', 'orange', 'grape']
print(fruits[:3])       # ['apple', 'banana', 'orange'] (first 3)
print(fruits[2:])       # ['orange', 'grape', 'mango'] (from index 2)
print(fruits[::2])      # ['apple', 'orange', 'mango'] (every 2nd)
print(fruits[::-1])     # ['mango', 'grape', 'orange', 'banana', 'apple'] (reversed)

# Practical example
numbers = list(range(1, 11))  # [1, 2, 3, ..., 10]
print(numbers[2:7])           # [3, 4, 5, 6, 7]
print(numbers[::3])           # [1, 4, 7, 10]
```

---

## Modifying Lists

### Adding Elements

```python
numbers = [1, 2, 3]

# append - add to end
numbers.append(4)
print(numbers)  # [1, 2, 3, 4]

# insert - add at position
numbers.insert(2, 2.5)
print(numbers)  # [1, 2, 2.5, 3, 4]

# extend - add multiple items
numbers.extend([5, 6, 7])
print(numbers)  # [1, 2, 2.5, 3, 4, 5, 6, 7]

# + operator
list1 = [1, 2, 3]
list2 = [4, 5, 6]
combined = list1 + list2
print(combined)  # [1, 2, 3, 4, 5, 6]
```

### Removing Elements

```python
numbers = [1, 2, 3, 4, 5, 3]

# remove - remove first occurrence
numbers.remove(3)
print(numbers)  # [1, 2, 4, 5, 3]

# pop - remove and return element at index
popped = numbers.pop()        # Remove last
print(popped)                 # 3
print(numbers)                # [1, 2, 4, 5]

popped = numbers.pop(1)       # Remove at index 1
print(popped)                 # 2
print(numbers)                # [1, 4, 5]

# del - delete by index
del numbers[0]
print(numbers)                # [4, 5]

# clear - remove all
numbers.clear()
print(numbers)                # []
```

### Modifying Elements

```python
numbers = [1, 2, 3, 4, 5]

# Change single element
numbers[2] = 30
print(numbers)  # [1, 2, 30, 4, 5]

# Change multiple elements (slice)
numbers[1:3] = [20, 30, 40]
print(numbers)  # [1, 20, 30, 40, 5]

# Replace with different length
numbers = [1, 2, 3, 4, 5]
numbers[1:4] = [20, 30]
print(numbers)  # [1, 20, 30, 5]
```

---

## List Methods

### Information Methods

```python
numbers = [1, 2, 3, 4, 5, 3, 3]

# len - length
print(len(numbers))         # 7

# count - occurrences
print(numbers.count(3))     # 3

# index - position of first occurrence
print(numbers.index(3))     # 2

# Check membership
print(3 in numbers)         # True
print(10 in numbers)        # False
print(10 not in numbers)    # True
```

### Sorting and Ordering

```python
numbers = [3, 1, 4, 1, 5, 9, 2, 6]

# sort - in-place sorting
numbers_copy = numbers.copy()
numbers_copy.sort()
print(numbers_copy)         # [1, 1, 2, 3, 4, 5, 6, 9]

# Reverse sort
numbers_copy.sort(reverse=True)
print(numbers_copy)         # [9, 6, 5, 4, 3, 2, 1, 1]

# reverse - in-place reversal
numbers_copy.reverse()
print(numbers_copy)         # [1, 1, 2, 3, 4, 5, 6, 9]

# sorted - returns new sorted list
numbers_sorted = sorted(numbers)
print(numbers_sorted)       # [1, 1, 2, 3, 4, 5, 6, 9]
print(numbers)              # [3, 1, 4, 1, 5, 9, 2, 6] (original unchanged)

# Sort with key function
words = ["apple", "pie", "zoo", "a"]
words_sorted = sorted(words, key=len)
print(words_sorted)         # ['a', 'pie', 'apple', 'zoo']
```

### Copying Lists

```python
# Shallow copy
original = [1, 2, [3, 4]]

# ❌ Wrong - same reference
copy1 = original
copy1[0] = 99
print(original)  # [99, 2, [3, 4]] (changed!)

# ✅ Correct methods
copy2 = original.copy()      # Shallow copy
copy3 = original[:]          # Shallow copy
copy4 = list(original)       # Shallow copy

import copy
copy5 = copy.deepcopy(original)  # Deep copy
```

---

## List Comprehension

### Basic Comprehension

```python
# Traditional
squares = []
for i in range(5):
    squares.append(i ** 2)

# Comprehension (shorter, more Pythonic)
squares = [i ** 2 for i in range(5)]
print(squares)  # [0, 1, 4, 9, 16]

# With condition
evens = [i for i in range(10) if i % 2 == 0]
print(evens)    # [0, 2, 4, 6, 8]

# Multiple conditions
numbers = [i for i in range(10) if i % 2 == 0 if i % 3 == 0]
print(numbers)  # [0, 6]
```

### Nested Comprehension

```python
# Create matrix
matrix = [[i + j for j in range(3)] for i in range(3)]
print(matrix)
# [[0, 1, 2], [1, 2, 3], [2, 3, 4]]

# Flatten list
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
flattened = [num for row in matrix for num in row]
print(flattened)  # [1, 2, 3, 4, 5, 6, 7, 8, 9]

# With transformation
words = ["hello", "world", "python"]
lengths = [len(word) for word in words]
print(lengths)    # [5, 5, 6]
```

---

## Iterating Over Lists

### for Loop

```python
numbers = [1, 2, 3, 4, 5]

# Basic iteration
for num in numbers:
    print(num)

# With index using enumerate
for index, num in enumerate(numbers):
    print(f"{index}: {num}")

# With starting index
for index, num in enumerate(numbers, start=1):
    print(f"{index}: {num}")
```

### Zip (Combine Lists)

```python
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30, 35]
cities = ["NYC", "LA", "Chicago"]

for name, age, city in zip(names, ages, cities):
    print(f"{name} is {age} and lives in {city}")

# Unequal length lists - stops at shortest
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30]

for name, age in zip(names, ages):
    print(f"{name}: {age}")
# Output:
# Alice: 25
# Bob: 30
```

---

## Practical Examples

### Student Grade Management

```python
students = ["Alice", "Bob", "Charlie", "Diana"]
grades = [85, 92, 78, 95]

# Display with grades
for i, student in enumerate(students):
    print(f"{i+1}. {student}: {grades[i]}")

# Find top student
top_index = grades.index(max(grades))
print(f"Top student: {students[top_index]}")

# Average grade
average = sum(grades) / len(grades)
print(f"Class average: {average:.2f}")

# Above average students
above_avg = [students[i] for i, grade in enumerate(grades) if grade >= average]
print(f"Above average: {above_avg}")
```

### Todo List

```python
todos = []

def add_todo(task):
    todos.append(task)
    print(f"Added: {task}")

def remove_todo(index):
    if 0 <= index < len(todos):
        removed = todos.pop(index)
        print(f"Removed: {removed}")

def show_todos():
    if not todos:
        print("No todos!")
    else:
        for i, todo in enumerate(todos, 1):
            print(f"{i}. {todo}")

add_todo("Buy groceries")
add_todo("Finish homework")
add_todo("Call mom")
show_todos()
remove_todo(1)
show_todos()
```

### Data Analysis

```python
sales_data = [100, 250, 180, 320, 410, 290, 500]

# Total and average
total = sum(sales_data)
average = total / len(sales_data)

# Max and min
max_sale = max(sales_data)
min_sale = min(sales_data)

# Above average
above_avg = [sale for sale in sales_data if sale > average]

print(f"Total sales: ${total}")
print(f"Average sale: ${average:.2f}")
print(f"Highest sale: ${max_sale}")
print(f"Lowest sale: ${min_sale}")
print(f"Above average sales: {above_avg}")
```

---

## Common Mistakes

```python
# ❌ Modifying list while iterating
numbers = [1, 2, 3, 4, 5]
for num in numbers:
    if num == 3:
        numbers.remove(num)  # Don't do this!

# ✅ Create new list instead
numbers = [1, 2, 3, 4, 5]
numbers = [num for num in numbers if num != 3]

# ❌ Index out of range
my_list = [1, 2, 3]
# print(my_list[5])  # Error!

# ✅ Check length first
if len(my_list) > 5:
    print(my_list[5])

# ❌ Mutable default argument
def add_item(item, lst=[]):
    lst.append(item)
    return lst

# ✅ Use None as default
def add_item(item, lst=None):
    if lst is None:
        lst = []
    lst.append(item)
    return lst
```

---

## Summary

| Operation | Example | Result |
|-----------|---------|--------|
| Create | `[1, 2, 3]` | List |
| Access | `list[0]` | First element |
| Slice | `list[1:3]` | Elements 1-2 |
| Append | `list.append(4)` | Add to end |
| Insert | `list.insert(0, 1)` | Add at position |
| Remove | `list.remove(2)` | Remove value |
| Pop | `list.pop()` | Remove & return |
| Sort | `list.sort()` | Sort in-place |
| Length | `len(list)` | Number of items |

---

**Next**: [Tuples](tuples.md)
