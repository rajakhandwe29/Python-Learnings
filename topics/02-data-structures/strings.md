# Strings in Python: A Comprehensive Guide

## Table of Contents
1. [Introduction](#introduction)
2. [String Creation](#string-creation)
3. [String Indexing and Slicing](#string-indexing-and-slicing)
4. [String Methods](#string-methods)
5. [String Formatting](#string-formatting)
6. [String Operations](#string-operations)
7. [Regular Expressions](#regular-expressions)
8. [Encoding and Decoding](#encoding-and-decoding)
9. [Text Processing](#text-processing)
10. [Common Mistakes](#common-mistakes)
11. [Best Practices](#best-practices)
12. [Performance Optimization](#performance-optimization)
13. [Summary](#summary)

## Introduction

Strings are sequences of Unicode characters and one of the most fundamental data types in Python. They're immutable, meaning once created, they cannot be changed. Strings support a rich set of methods and operations, making text manipulation both powerful and intuitive.

### Why Strings Matter

Strings are essential for:
- Processing text data
- Reading and writing files
- Formatting output
- Web development and APIs
- Data validation
- Natural language processing

### Quick Example

```python
# Creating strings
message = "Hello, World!"
name = 'Alice'
multiline = """This is
a multi-line
string"""

# String operations
greeting = "Hello " + name
print(greeting)  # Output: Hello Alice

# String methods
text = "Python Programming"
print(text.lower())      # Output: python programming
print(text.replace("Programming", "Development"))  # Output: Python Development
```

## String Creation

### Literal Syntax

```python
# Single quotes
single = 'Hello'

# Double quotes
double = "World"

# Triple quotes (multi-line)
multiline = """This is a
multi-line string
that spans lines"""

# Triple single quotes (also multi-line)
also_multiline = '''Another
multi-line
string'''

# Raw strings (escape sequences not processed)
raw = r"C:\Users\Name\file.txt"  # Backslashes not escaped
print(raw)  # Output: C:\Users\Name\file.txt

# F-strings (formatted string literals)
name = "Bob"
age = 30
formatted = f"{name} is {age} years old"
print(formatted)  # Output: Bob is 30 years old
```

### Escape Sequences

```python
# Common escape sequences
text = "Line 1\nLine 2"  # \n = newline
print(text)
# Output:
# Line 1
# Line 2

text = "Hello\tWorld"  # \t = tab
print(text)  # Output: Hello	World

text = "Quote: \"Hello\""  # \" = escaped quote
print(text)  # Output: Quote: "Hello"

text = "Path: C:\\Users\\Name"  # \\ = backslash
print(text)  # Output: Path: C:\Users\Name

text = "Unicode: \u0041"  # \u = unicode
print(text)  # Output: Unicode: A
```

### Concatenation

```python
# String concatenation
first = "Hello"
second = "World"
combined = first + " " + second
print(combined)  # Output: Hello World

# Inefficient for many strings (creates intermediate strings)
# BAD:
result = ""
for i in range(1000000):
    result += str(i)  # Creates new string each time!

# GOOD:
result = "".join(str(i) for i in range(1000000))

# String repetition
repeated = "Ha" * 3
print(repeated)  # Output: HaHaHa
```

## String Indexing and Slicing

### Indexing

```python
text = "Python"

# Positive indexing (left to right)
print(text[0])  # Output: P
print(text[2])  # Output: t
print(text[5])  # Output: n

# Negative indexing (right to left)
print(text[-1])  # Output: n
print(text[-3])  # Output: h
print(text[-6])  # Output: P

# Out of bounds raises IndexError
try:
    print(text[10])
except IndexError:
    print("Index out of range")
```

### Slicing

```python
text = "Python Programming"

# Basic slicing [start:end:step]
print(text[0:6])      # Output: Python
print(text[7:18])     # Output: Programming
print(text[:6])       # Output: Python
print(text[7:])       # Output: Programming

# Slicing with step
print(text[::2])      # Output: Pto rgamn (every 2nd char)
print(text[1::2])     # Output: yhnoogram (every 2nd, starting at 1)
print(text[::-1])     # Output: gnimmargorP nohtyP (reversed)

# Negative slicing
print(text[-11:])     # Output: Programming
print(text[:-11])     # Output: Python 
print(text[-1::-1])   # Output: gnimmargorP nohtyP (reversed, excluding first)
```

## String Methods

### Case Conversion

```python
text = "Python"

# Convert to lowercase
print(text.lower())        # Output: python

# Convert to uppercase
print(text.upper())        # Output: PYTHON

# Swap case
print(text.swapcase())     # Output: pYTHON

# Title case (capitalize first letter of each word)
sentence = "hello world python"
print(sentence.title())    # Output: Hello World Python

# Capitalize (first character only)
print(sentence.capitalize())  # Output: Hello world python
```

### Searching and Finding

```python
text = "The quick brown fox jumps over the lazy dog"

# Find substring (returns index or -1)
print(text.find("quick"))      # Output: 4
print(text.find("python"))     # Output: -1 (not found)

# Find with error
try:
    print(text.index("python"))
except ValueError:
    print("Substring not found")

# Find starting from position
print(text.find("the", 0))     # Output: 0 (first 'the')
print(text.find("the", 1))     # Output: 40 (second 'the')

# Count occurrences
print(text.count("o"))         # Output: 4
print(text.count("the"))       # Output: 2

# Check if string starts or ends with
print(text.startswith("The"))  # Output: True
print(text.endswith("dog"))    # Output: True
print(text.endswith("cat"))    # Output: False
```

### String Splitting and Joining

```python
# Split string into list
text = "apple,banana,cherry"
fruits = text.split(",")
print(fruits)  # Output: ['apple', 'banana', 'cherry']

# Split with limit
parts = text.split(",", 1)
print(parts)  # Output: ['apple', 'banana,cherry']

# Split on whitespace (default)
sentence = "The quick brown fox"
words = sentence.split()
print(words)  # Output: ['The', 'quick', 'brown', 'fox']

# Join list into string
words = ["hello", "world", "python"]
result = " ".join(words)
print(result)  # Output: hello world python

# Join with different separator
result = "-".join(words)
print(result)  # Output: hello-world-python

# Multiline join
lines = ["Line 1", "Line 2", "Line 3"]
result = "\n".join(lines)
print(result)
# Output:
# Line 1
# Line 2
# Line 3
```

### Whitespace Handling

```python
# Remove leading and trailing whitespace
text = "  Hello World  "
print(f"'{text.strip()}'")    # Output: 'Hello World'
print(f"'{text.lstrip()}'")   # Output: 'Hello World  '
print(f"'{text.rstrip()}'")   # Output: '  Hello World'

# Remove specific characters
text = "***Hello***"
print(text.strip("*"))  # Output: Hello

# Replace method
text = "The quick brown fox"
print(text.replace("quick", "slow"))   # Output: The slow brown fox
print(text.replace("o", "0"))          # Output: The quick br0wn f0x

# Replace with limit
print(text.replace("o", "0", 1))       # Output: The quick br0wn fox
```

### Checking String Contents

```python
text = "Hello123"

# Check if all characters are...
print("hello".isalpha())       # Output: True (all letters)
print("hello123".isalnum())    # Output: True (letters and digits)
print("12345".isdigit())       # Output: True (all digits)
print("   ".isspace())         # Output: True (all whitespace)
print("Hello".isupper())       # Output: False (not all uppercase)
print("HELLO".isupper())       # Output: True
print("hello".islower())       # Output: True
print("Title".istitle())       # Output: True

# Check if empty
print(len("") == 0)            # Output: True
print("text" != "")            # Output: True
```

## String Formatting

### F-strings (Python 3.6+)

```python
# Basic f-string
name = "Alice"
age = 30
print(f"{name} is {age} years old")
# Output: Alice is 30 years old

# Expressions in f-strings
x = 10
y = 20
print(f"{x} + {y} = {x + y}")
# Output: 10 + 20 = 30

# Formatting options
price = 19.99
print(f"Price: ${price:.2f}")  # 2 decimal places
# Output: Price: $19.99

# Alignment and padding
text = "Hello"
print(f"{text:>10}")   # Right align in 10 chars
print(f"{text:<10}")   # Left align in 10 chars
print(f"{text:^10}")   # Center in 10 chars

# Number formatting
num = 1234567
print(f"Number: {num:,}")       # Output: Number: 1,234,567
print(f"Percent: {0.75:.0%}")   # Output: Percent: 75%
print(f"Scientific: {1000:.2e}") # Output: Scientific: 1.00e+03

# Debug with f-strings (Python 3.8+)
name = "Bob"
print(f"{name=}")  # Output: name='Bob'
```

### .format() Method

```python
# Basic formatting
text = "{} is {} years old"
print(text.format("Charlie", 25))
# Output: Charlie is 25 years old

# Named placeholders
text = "{name} is {age} years old"
print(text.format(name="David", age=28))
# Output: David is 28 years old

# Index-based
text = "{0} and {1} are friends"
print(text.format("Eve", "Frank"))
# Output: Eve and Frank are friends

# Format specifications
print("{:.2f}".format(3.14159))      # Output: 3.14
print("{:>10}".format("text"))       # Right align
print("{:,}".format(1000000))        # Output: 1,000,000
```

### % Operator (older style)

```python
# String interpolation with %
text = "%s is %d years old" % ("Grace", 32)
print(text)  # Output: Grace is 32 years old

# Multiple values
text = "%s, %s, %.2f" % ("one", "two", 3.14159)
print(text)  # Output: one, two, 3.14
```

## String Operations

### Membership Testing

```python
text = "Python Programming"

# Check if substring in string
print("Python" in text)        # Output: True
print("java" in text)          # Output: False
print("Python" not in text)    # Output: False

# Case-sensitive
print("python" in text)        # Output: False (lowercase)
```

### Iteration

```python
# Iterate over characters
for char in "Hello":
    print(char)
# Output:
# H
# e
# l
# l
# o

# Iterate with index
text = "abc"
for i, char in enumerate(text):
    print(f"{i}: {char}")
# Output:
# 0: a
# 1: b
# 2: c

# Reverse iteration
for char in reversed("hello"):
    print(char, end="")
# Output: olleh
```

### String Length

```python
text = "Hello"
print(len(text))  # Output: 5

# Length of unicode strings
emoji = "😀"
print(len(emoji))  # Output: 1

# Empty string
empty = ""
print(len(empty))  # Output: 0
```

## Regular Expressions

### Basic Regex

```python
import re

# Simple pattern matching
pattern = r"hello"
text = "hello world"
if re.search(pattern, text):
    print("Pattern found!")  # Output: Pattern found!

# Case-insensitive
pattern = r"hello"
text = "Hello World"
match = re.search(pattern, text, re.IGNORECASE)
print(match)  # Output: <re.Match object; span=(0, 5), match='Hello'>

# Get matched text
print(match.group())  # Output: Hello
```

### Pattern Matching

```python
import re

text = "My phone is 123-456-7890"

# Find pattern
pattern = r"\d{3}-\d{3}-\d{4}"  # Phone number pattern
match = re.search(pattern, text)
if match:
    print(f"Phone: {match.group()}")  # Output: Phone: 123-456-7890

# Find all matches
text = "I have 2 apples and 5 oranges"
pattern = r"\d+"
numbers = re.findall(pattern, text)
print(numbers)  # Output: ['2', '5']

# Replace matches
text = "Color: blue"
result = re.sub(r"blue", "red", text)
print(result)  # Output: Color: red

# Split by pattern
text = "apple, banana; orange"
fruits = re.split(r"[,;]", text)
print(fruits)  # Output: ['apple', ' banana', ' orange']
```

### Email and URL Validation

```python
import re

# Simple email validation
email_pattern = r"^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$"

emails = [
    "alice@example.com",
    "bob.smith@gmail.co.uk",
    "invalid@",
    "noatsign.com"
]

for email in emails:
    if re.match(email_pattern, email):
        print(f"✓ Valid: {email}")
    else:
        print(f"✗ Invalid: {email}")

# URL validation
url_pattern = r"^https?://[^\s/$.?#].[^\s]*$"
urls = [
    "https://example.com",
    "http://sub.example.org/path",
    "not a url"
]

for url in urls:
    if re.match(url_pattern, url):
        print(f"✓ Valid URL: {url}")
```

## Encoding and Decoding

### UTF-8 Encoding

```python
# Encode string to bytes
text = "Hello, 世界"
encoded = text.encode("utf-8")
print(encoded)  # Output: b'Hello, \xe4\xb8\x96\xe7\x95\x8c'

# Decode bytes to string
decoded = encoded.decode("utf-8")
print(decoded)  # Output: Hello, 世界

# Different encodings
text = "café"
print(text.encode("utf-8"))    # Output: b'caf\xc3\xa9'
print(text.encode("ascii"))    # UnicodeEncodeError!

# Handle encoding errors
try:
    text.encode("ascii")
except UnicodeEncodeError:
    encoded = text.encode("ascii", errors="ignore")
    print(encoded)  # Output: b'caf'
```

## Text Processing

### Word Frequency Analysis

```python
from collections import Counter
import re

text = """Python is a powerful language.
Python is widely used for web development.
Python is great for data science."""

# Extract words (lowercase, remove punctuation)
words = re.findall(r"\b\w+\b", text.lower())
print(words)

# Count frequency
word_freq = Counter(words)
print(word_freq.most_common(5))
# Output: [('python', 3), ('is', 3), ('for', 2), ('a', 1), ('powerful', 1)]
```

### Text Cleaning

```python
import re

def clean_text(text):
    # Convert to lowercase
    text = text.lower()
    
    # Remove special characters
    text = re.sub(r"[^a-z\s]", "", text)
    
    # Remove extra whitespace
    text = " ".join(text.split())
    
    return text

messy = "Hello! @#$ WORLD... 123"
cleaned = clean_text(messy)
print(cleaned)  # Output: hello world
```

## Common Mistakes

### Mistake 1: Thinking Strings are Mutable

```python
# WRONG - strings are immutable
text = "hello"
# text[0] = "H"  # TypeError: 'str' object does not support item assignment

# CORRECT - create new string
text = "hello"
text = text[0].upper() + text[1:]
print(text)  # Output: Hello
```

### Mistake 2: Not Joining Strings Efficiently

```python
# WRONG - inefficient concatenation
result = ""
for i in range(10000):
    result += str(i)  # Creates new string each time O(n²)!

# CORRECT - use join
result = "".join(str(i) for i in range(10000))
```

### Mistake 3: Empty Set vs Empty String

```python
# WRONG
empty_dict = {}  # This is a dict!

# CORRECT for dict
empty_dict = {}

# Strings have different syntax
empty_string = ""

# Be aware of truthiness
if "":  # Empty string is falsy
    print("This won't print")
else:
    print("Empty string is falsy")  # This prints
```

### Mistake 4: Case Sensitivity

```python
# WRONG - assuming case-insensitive
text = "Python"
if "python" in text:  # False! Case-sensitive
    print("Found")

# CORRECT - handle case
if "python" in text.lower():
    print("Found")  # This prints
```

### Mistake 5: Regex Without Raw String

```python
# WRONG - backslashes interpreted as escape sequences
pattern = "\d+"  # This becomes just "d+"!

# CORRECT - use raw string
pattern = r"\d+"  # Now it's a valid digit pattern
```

## Best Practices

### 1. Use F-strings for Formatting

```python
# Good - readable and concise
name = "Alice"
age = 30
print(f"{name} is {age} years old")

# Less good - older style
print("{} is {} years old".format(name, age))

# Avoid - % operator is outdated
# print("%s is %d years old" % (name, age))
```

### 2. Use .join() for Concatenation

```python
# Good - efficient
words = ["hello", "world", "python"]
result = " ".join(words)

# Bad - inefficient
result = ""
for word in words:
    result += word + " "
```

### 3. Use in Operator for Substring

```python
# Good - clear and efficient
if "error" in log_message:
    print("Error found")

# Less good - using find
if log_message.find("error") != -1:
    print("Error found")
```

### 4. Use Raw Strings for Regex

```python
# Good - raw string for regex
pattern = r"\d{3}-\d{3}-\d{4}"

# Bad - backslashes create confusion
pattern = "\\d{3}-\\d{3}-\\d{4}"
```

## Performance Optimization

### String Concatenation Performance

```python
import timeit

# Inefficient
def concat_bad():
    result = ""
    for i in range(1000):
        result += str(i)
    return result

# Efficient
def concat_good():
    return "".join(str(i) for i in range(1000))

bad_time = timeit.timeit(concat_bad, number=100)
good_time = timeit.timeit(concat_good, number=100)

print(f"Inefficient: {bad_time:.4f}s")
print(f"Efficient: {good_time:.4f}s")
# Efficient is significantly faster!
```

## Summary

| Operation | Example | Result |
|-----------|---------|--------|
| **Creation** | `"hello"` or `f"{var}"` | String |
| **Indexing** | `text[0]` | First character |
| **Slicing** | `text[1:5]` | Substring |
| **Length** | `len(text)` | Number of characters |
| **Find** | `text.find("o")` | Index or -1 |
| **Replace** | `text.replace("a", "b")` | New string |
| **Split** | `text.split(",")` | List |
| **Join** | `", ".join(list)` | String |
| **Case** | `text.upper()` / `text.lower()` | String |
| **Strip** | `text.strip()` | Trimmed string |
| **Format** | `f"{var}"` | Formatted string |

### Key Takeaways

1. **Strings are immutable** - operations return new strings
2. **Use f-strings for formatting** - most readable and efficient
3. **Use .join() for concatenation** - much faster than += operator
4. **Use raw strings for regex** - prevents escape sequence confusion
5. **Strings are ordered and indexable** - support slicing and iteration
6. **String methods are powerful** - learn common ones for efficiency
7. **Unicode support is automatic** - Python 3 handles UTF-8 natively

### Practice Exercises

1. Create a function to capitalize the first letter of each word
2. Write a URL slug generator that converts text to URL-safe format
3. Implement a simple email validator using regex
4. Create a text analysis tool showing word frequency
5. Build a CSV parser that handles quoted fields

---

**Next:** Explore more data structures or move to Object-Oriented Programming for advanced Python concepts.
