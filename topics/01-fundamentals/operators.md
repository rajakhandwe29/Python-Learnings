# Operators

Learn how to perform operations on data using Python operators.

## Table of Contents
1. [Arithmetic Operators](#arithmetic-operators)
2. [Comparison Operators](#comparison-operators)
3. [Logical Operators](#logical-operators)
4. [Membership Operators](#membership-operators)
5. [Identity Operators](#identity-operators)
6. [Bitwise Operators](#bitwise-operators)
7. [Operator Precedence](#operator-precedence)

---

## Arithmetic Operators

Operations on numeric values.

```python
# Basic arithmetic
a = 10
b = 3

print(a + b)    # 13 (addition)
print(a - b)    # 7 (subtraction)
print(a * b)    # 30 (multiplication)
print(a / b)    # 3.333... (true division)
print(a // b)   # 3 (floor division)
print(a % b)    # 1 (modulo - remainder)
print(a ** b)   # 1000 (exponentiation)

# Unary operators
x = 5
print(+x)       # 5 (unary plus)
print(-x)       # -5 (unary minus)
```

### Practical Examples

```python
# Calculate area of rectangle
length = 10
width = 5
area = length * width
print(f"Area: {area}")  # Area: 50

# Calculate percentage
total = 100
percentage = 20
result = (percentage / total) * 100
print(f"{percentage}% of {total} = {result}%")

# Temperature conversion
celsius = 25
fahrenheit = (celsius * 9/5) + 32
print(f"{celsius}°C = {fahrenheit}°F")

# Check if number is even or odd
number = 10
if number % 2 == 0:
    print("Even")
else:
    print("Odd")
```

### Augmented Assignment

```python
x = 10

x += 5      # x = x + 5 → 15
x -= 3      # x = x - 3 → 12
x *= 2      # x = x * 2 → 24
x /= 4      # x = x / 4 → 6.0
x //= 2     # x = x // 2 → 3.0
x **= 2     # x = x ** 2 → 9.0
x %= 5      # x = x % 5 → 4.0
```

---

## Comparison Operators

Compare two values and return boolean results.

```python
a = 10
b = 5

# Comparison
print(a == b)   # False (equal)
print(a != b)   # True (not equal)
print(a > b)    # True (greater than)
print(a < b)    # False (less than)
print(a >= b)   # True (greater than or equal)
print(a <= b)   # False (less than or equal)

# String comparison
print("apple" == "apple")      # True
print("apple" != "banana")     # True
print("apple" < "banana")      # True (alphabetically)

# Chain comparison
age = 25
print(18 < age < 65)           # True (equivalent to: age > 18 and age < 65)
print(0 <= age <= 100)         # True

# List comparison
list1 = [1, 2, 3]
list2 = [1, 2, 3]
print(list1 == list2)          # True (same contents)
print(list1 is list2)          # False (different objects)
```

### Practical Examples

```python
# Age verification
user_age = 25
if user_age >= 18:
    print("Access granted")
else:
    print("Access denied")

# Grading system
score = 85
if score >= 90:
    grade = "A"
elif score >= 80:
    grade = "B"
elif score >= 70:
    grade = "C"
else:
    grade = "F"
print(f"Grade: {grade}")

# Range checking
number = 50
if 1 <= number <= 100:
    print("Number is in valid range")
```

---

## Logical Operators

Combine boolean values.

```python
# AND operator - both conditions must be True
a = True
b = False
print(a and b)      # False
print(a and True)   # True

# OR operator - at least one condition must be True
print(a or b)       # True
print(False or False)  # False

# NOT operator - reverses boolean value
print(not a)        # False
print(not b)        # True
```

### Practical Examples

```python
# Login validation
username = "admin"
password = "secret"

if username == "admin" and password == "secret":
    print("Login successful")
else:
    print("Invalid credentials")

# User eligibility
age = 25
has_license = True

if age >= 18 and has_license:
    print("Can drive")
else:
    print("Cannot drive")

# Input validation
email = "user@example.com"
has_domain = "@" in email
has_extension = "." in email

if email and has_domain and has_extension:
    print("Valid email format")
else:
    print("Invalid email")

# Permission checking
is_admin = True
is_owner = False

if is_admin or is_owner:
    print("Has access")
else:
    print("Access denied")
```

### Short-Circuit Evaluation

```python
# AND - stops evaluating if first is False
def test_function():
    print("Function called")
    return True

result = False and test_function()  # Function NOT called (short-circuit)

# OR - stops evaluating if first is True
result = True or test_function()    # Function NOT called (short-circuit)

# Practical use
user_data = None
if user_data and user_data["name"]:  # Safe - won't error if user_data is None
    print(user_data["name"])
```

---

## Membership Operators

Check if a value exists in a sequence.

```python
# in operator
numbers = [1, 2, 3, 4, 5]
print(3 in numbers)        # True
print(10 in numbers)       # False

text = "Hello"
print("H" in text)         # True
print("x" in text)         # False

# not in operator
print(10 not in numbers)   # True
print(3 not in numbers)    # False
```

### Practical Examples

```python
# Check if item in list
shopping_list = ["apple", "banana", "orange"]

if "apple" in shopping_list:
    print("Apple is in the list")

# Check if key in dictionary
user = {"name": "John", "age": 25, "email": "john@email.com"}

if "email" in user:
    print(f"Email: {user['email']}")

# Case-insensitive search
available_colors = ["red", "blue", "green"]
color_input = "RED"

if color_input.lower() in available_colors:
    print("Color available")

# Substring check
text = "Python is awesome"
if "awesome" in text:
    print("Found!")
```

---

## Identity Operators

Check if two variables refer to the same object.

```python
a = [1, 2, 3]
b = [1, 2, 3]
c = a

# is operator - checks if same object
print(a is b)       # False (different objects)
print(a is c)       # True (same object)

# is not operator
print(a is not b)   # True
print(a is not c)   # False

# String interning (Python optimization)
x = "hello"
y = "hello"
print(x is y)       # Usually True (strings are cached)

# None checking
value = None
print(value is None)        # True
print(value is not None)    # False
```

### Important: == vs is

```python
# == checks VALUE equality
# is checks OBJECT identity

list1 = [1, 2, 3]
list2 = [1, 2, 3]

print(list1 == list2)       # True (same contents)
print(list1 is list2)       # False (different objects)

# Correct way to check for None
value = None
if value is None:           # ✅ Correct
    print("Value is None")

# Don't do this
if value == None:           # ❌ Works but not Pythonic
    print("Value is None")
```

---

## Bitwise Operators

Operations on binary representations of numbers.

```python
a = 12      # Binary: 1100
b = 10      # Binary: 1010

# AND - both bits must be 1
print(a & b)    # 8 (Binary: 1000)

# OR - at least one bit is 1
print(a | b)    # 14 (Binary: 1110)

# XOR - bits must be different
print(a ^ b)    # 6 (Binary: 0110)

# NOT - inverts bits
print(~a)       # -13 (Binary: ~1100)

# Left shift - multiply by 2
print(a << 1)   # 24 (12 * 2)

# Right shift - divide by 2
print(a >> 1)   # 6 (12 // 2)
```

### Practical Examples

```python
# Checking if power of 2
def is_power_of_2(n):
    return n > 0 and (n & (n - 1)) == 0

print(is_power_of_2(8))    # True
print(is_power_of_2(6))    # False

# Swapping without temp variable
a = 5
b = 10
a, b = a ^ b, a ^ b ^ a   # XOR swap
print(a, b)  # 10, 5

# Counting set bits
def count_bits(n):
    count = 0
    while n:
        count += n & 1
        n >>= 1
    return count

print(count_bits(7))  # 3 (111 in binary)
```

---

## Operator Precedence

Order in which operators are evaluated.

```python
# Higher precedence = evaluated first

print(2 + 3 * 4)        # 14 (multiplication before addition)
print((2 + 3) * 4)      # 20 (parentheses first)

result = 10 + 5 * 2 - 3
# = 10 + 10 - 3
# = 20 - 3
# = 17
print(result)

# Precedence order (highest to lowest):
# 1. ** (exponentiation)
# 2. +x, -x, ~x (unary)
# 3. *, /, //, % (multiplication, division)
# 4. +, - (addition, subtraction)
# 5. <<, >> (bitwise shifts)
# 6. & (bitwise AND)
# 7. ^ (bitwise XOR)
# 8. | (bitwise OR)
# 9. ==, !=, <, >, <=, >= (comparisons)
# 10. is, is not, in, not in (identity, membership)
# 11. not (logical NOT)
# 12. and (logical AND)
# 13. or (logical OR)
```

### Complex Examples

```python
# Example 1
result = 2 + 3 * 4 ** 2 - 5
# = 2 + 3 * 16 - 5
# = 2 + 48 - 5
# = 45
print(result)

# Example 2
x = 10
print(x > 5 and x < 20 or x == 100)  # True
# = (10 > 5 and 10 < 20) or 10 == 100
# = (True and True) or False
# = True or False
# = True

# Example 3 - Use parentheses for clarity
result = (10 + 5) * 2
print(result)  # 30
```

---

## Best Practices

### 1. Use Parentheses for Clarity
```python
# ❌ Hard to read
result = 10 + 5 * 2 - 3 / 2

# ✅ Clear
result = (10 + (5 * 2)) - (3 / 2)
```

### 2. Avoid Complex Conditions
```python
# ❌ Hard to understand
if age >= 18 and has_license and not is_suspended and is_sober:
    pass

# ✅ Better - use helper variable/function
can_drive = age >= 18 and has_license
is_allowed = not is_suspended and is_sober

if can_drive and is_allowed:
    pass
```

### 3. Use Appropriate Operators
```python
# ✅ Correct - use 'in' for membership
if item in list:
    pass

# ✅ Correct - use 'is' for None
if value is None:
    pass

# ❌ Avoid comparing with True/False
if condition == True:  # Don't do this
    pass

# ✅ Better
if condition:
    pass
```

---

## Summary

| Operator | Type | Example | Result |
|----------|------|---------|--------|
| + | Arithmetic | 5 + 3 | 8 |
| - | Arithmetic | 5 - 3 | 2 |
| * | Arithmetic | 5 * 3 | 15 |
| / | Arithmetic | 5 / 2 | 2.5 |
| // | Arithmetic | 5 // 2 | 2 |
| % | Arithmetic | 5 % 2 | 1 |
| ** | Arithmetic | 5 ** 2 | 25 |
| == | Comparison | 5 == 5 | True |
| != | Comparison | 5 != 3 | True |
| > | Comparison | 5 > 3 | True |
| < | Comparison | 5 < 3 | False |
| >= | Comparison | 5 >= 5 | True |
| <= | Comparison | 5 <= 3 | False |
| and | Logical | True and False | False |
| or | Logical | True or False | True |
| not | Logical | not True | False |
| in | Membership | 3 in [1,2,3] | True |
| is | Identity | a is b | Depends |

---

## Practice Exercises

1. **Arithmetic**: Calculate area and perimeter of shapes
2. **Comparison**: Build a simple grade calculator
3. **Logical**: Create login validation logic
4. **Membership**: Search items in lists
5. **Complex**: Build a compound condition checker

---

**Next**: [Control Flow](control-flow.md)
