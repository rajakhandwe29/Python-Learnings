# Control Flow

Master decision-making and looping structures in Python.

## Table of Contents
1. [if Statements](#if-statements)
2. [while Loops](#while-loops)
3. [for Loops](#for-loops)
4. [Loop Control](#loop-control)
5. [Exception Handling Basics](#exception-handling-basics)

---

## if Statements

Execute code based on conditions.

### Simple if

```python
age = 18

if age >= 18:
    print("You are an adult")

# More complex
temperature = 25

if temperature > 30:
    print("It's hot!")
    print("Drink water!")
```

### if-else

```python
age = 15

if age >= 18:
    print("You can vote")
else:
    print("You cannot vote yet")

# Ternary operator (one-liner if-else)
status = "Adult" if age >= 18 else "Minor"
print(status)
```

### if-elif-else

```python
score = 85

if score >= 90:
    grade = "A"
elif score >= 80:
    grade = "B"
elif score >= 70:
    grade = "C"
elif score >= 60:
    grade = "D"
else:
    grade = "F"

print(f"Your grade is: {grade}")
```

### Nested if

```python
age = 25
has_license = True
is_sober = True

if age >= 18:
    if has_license:
        if is_sober:
            print("Can drive")
        else:
            print("Cannot drive - not sober")
    else:
        print("Cannot drive - no license")
else:
    print("Too young to drive")

# Better way - use logical operators
if age >= 18 and has_license and is_sober:
    print("Can drive")
```

### Practical Examples

```python
# User authentication
username_input = "admin"
password_input = "password123"

correct_username = "admin"
correct_password = "password123"

if username_input == correct_username:
    if password_input == correct_password:
        print("Login successful!")
    else:
        print("Wrong password")
else:
    print("User not found")

# ATM withdrawal
balance = 5000
withdrawal_amount = 2000

if withdrawal_amount > 0:
    if withdrawal_amount <= balance:
        balance -= withdrawal_amount
        print(f"Withdrawal successful. New balance: {balance}")
    else:
        print("Insufficient funds")
else:
    print("Invalid amount")

# Traffic light
light_color = "red"

if light_color == "red":
    action = "Stop"
elif light_color == "yellow":
    action = "Caution"
elif light_color == "green":
    action = "Go"
else:
    action = "Invalid color"

print(f"Traffic light is {light_color}: {action}")
```

---

## while Loops

Repeat code while a condition is true.

### Basic while

```python
count = 0
while count < 5:
    print(f"Count: {count}")
    count += 1

# Output:
# Count: 0
# Count: 1
# Count: 2
# Count: 3
# Count: 4
```

### Input Validation

```python
# Keep asking until valid input
while True:
    try:
        age = int(input("Enter your age: "))
        if 0 < age < 120:
            print(f"You are {age} years old")
            break  # Exit loop
        else:
            print("Age must be between 0 and 120")
    except ValueError:
        print("Please enter a valid number")
```

### Practical Examples

```python
# Counting game
secret_number = 7
guess = 0
attempts = 0

while guess != secret_number:
    guess = int(input("Guess the number (1-10): "))
    attempts += 1
    
    if guess < secret_number:
        print("Too low!")
    elif guess > secret_number:
        print("Too high!")
    else:
        print(f"Correct! You guessed in {attempts} attempts")

# Factorial calculation
number = 5
factorial = 1
original = number

while number > 0:
    factorial *= number
    number -= 1

print(f"Factorial of {original} is {factorial}")

# Sum user inputs until 0
total = 0
while True:
    number = int(input("Enter a number (0 to stop): "))
    if number == 0:
        break
    total += number

print(f"Total sum: {total}")
```

---

## for Loops

Iterate over sequences (lists, tuples, strings, ranges).

### Basic for Loop

```python
# Loop over list
fruits = ["apple", "banana", "orange"]
for fruit in fruits:
    print(fruit)

# Loop over string
word = "Python"
for letter in word:
    print(letter)

# Loop over range
for i in range(5):
    print(i)
# Output: 0, 1, 2, 3, 4

# Range with start and stop
for i in range(1, 5):
    print(i)
# Output: 1, 2, 3, 4

# Range with step
for i in range(0, 10, 2):
    print(i)
# Output: 0, 2, 4, 6, 8
```

### Enumerate (Index and Value)

```python
fruits = ["apple", "banana", "orange"]

for index, fruit in enumerate(fruits):
    print(f"{index}: {fruit}")

# Output:
# 0: apple
# 1: banana
# 2: orange

# With start index
for index, fruit in enumerate(fruits, start=1):
    print(f"{index}: {fruit}")
```

### Zip (Combine Lists)

```python
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30, 35]
cities = ["NYC", "LA", "Chicago"]

for name, age, city in zip(names, ages, cities):
    print(f"{name} is {age} and lives in {city}")

# Output:
# Alice is 25 and lives in NYC
# Bob is 30 and lives in LA
# Charlie is 35 and lives in Chicago
```

### Nested Loops

```python
# Multiplication table
for i in range(1, 4):
    for j in range(1, 4):
        print(f"{i} x {j} = {i*j}", end="  ")
    print()  # New line

# Output:
# 1 x 1 = 1  1 x 2 = 2  1 x 3 = 3  
# 2 x 1 = 2  2 x 2 = 4  2 x 3 = 6  
# 3 x 1 = 3  3 x 2 = 6  3 x 3 = 9  

# List of lists
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

for row in matrix:
    for num in row:
        print(num, end=" ")
    print()
```

### List Comprehension

```python
# Traditional way
squares = []
for i in range(5):
    squares.append(i ** 2)

# List comprehension (more Pythonic)
squares = [i ** 2 for i in range(5)]
print(squares)  # [0, 1, 4, 9, 16]

# With condition
evens = [i for i in range(10) if i % 2 == 0]
print(evens)  # [0, 2, 4, 6, 8]

# Nested list comprehension
matrix = [[i+j for j in range(3)] for i in range(3)]
print(matrix)
# [[0, 1, 2], [1, 2, 3], [2, 3, 4]]
```

### Practical Examples

```python
# Sum all numbers in a list
numbers = [1, 2, 3, 4, 5]
total = 0
for num in numbers:
    total += num
print(f"Sum: {total}")  # 15

# Find maximum
numbers = [3, 7, 2, 9, 1]
max_num = numbers[0]
for num in numbers:
    if num > max_num:
        max_num = num
print(f"Maximum: {max_num}")  # 9

# Process user data
users = [
    {"name": "Alice", "age": 25},
    {"name": "Bob", "age": 30},
    {"name": "Charlie", "age": 35}
]

for user in users:
    print(f"{user['name']}: {user['age']} years old")

# Count occurrences
text = "mississippi"
char_count = {}
for char in text:
    if char in char_count:
        char_count[char] += 1
    else:
        char_count[char] = 1
print(char_count)
```

---

## Loop Control

Control loop flow with break and continue.

### break

Exit the loop immediately.

```python
# Find a number in list
numbers = [2, 4, 6, 8, 9, 10]

for num in numbers:
    if num == 9:
        print(f"Found {num}!")
        break  # Exit loop
    print(num)

# Output:
# 2
# 4
# 6
# 8
# Found 9!

# Practical: Search for item
shopping_list = ["apple", "banana", "orange", "grape"]
item_to_find = "orange"

for item in shopping_list:
    if item == item_to_find:
        print(f"Found {item}!")
        break
else:
    print(f"{item_to_find} not found")
```

### continue

Skip current iteration and go to next.

```python
# Skip even numbers
for i in range(10):
    if i % 2 == 0:
        continue  # Skip this iteration
    print(i)

# Output: 1, 3, 5, 7, 9

# Skip invalid data
data = [1, -2, 3, -4, 5]

for num in data:
    if num < 0:
        continue  # Skip negative numbers
    print(f"Processing: {num}")
```

### for-else

Execute code if loop completes without break.

```python
# Search example
numbers = [2, 4, 6, 8, 10]
search_value = 7

for num in numbers:
    if num == search_value:
        print("Found!")
        break
else:
    print("Not found")

# Output: Not found

# Another example
numbers = [2, 4, 6, 8, 10]
search_value = 6

for num in numbers:
    if num == search_value:
        print("Found!")
        break
else:
    print("Not found")

# Output: Found!
```

---

## Exception Handling Basics

Handle errors gracefully.

```python
# Simple try-except
try:
    age = int(input("Enter your age: "))
except ValueError:
    print("Please enter a valid number")

# Multiple exceptions
try:
    numbers = [1, 2, 3]
    print(numbers[10])  # IndexError
except (IndexError, ValueError) as e:
    print(f"Error: {e}")

# Catch all exceptions (not recommended)
try:
    result = 10 / 0
except Exception as e:
    print(f"An error occurred: {e}")

# try-except-else
try:
    number = int(input("Enter a number: "))
except ValueError:
    print("Invalid input")
else:
    print(f"You entered: {number}")
```

---

## Practical Real-World Examples

### Login System
```python
max_attempts = 3
attempts = 0

while attempts < max_attempts:
    username = input("Username: ")
    password = input("Password: ")
    
    if username == "admin" and password == "1234":
        print("Login successful!")
        break
    else:
        attempts += 1
        remaining = max_attempts - attempts
        if remaining > 0:
            print(f"Invalid credentials. {remaining} attempts remaining.")
        else:
            print("Account locked!")
```

### Grade Calculator
```python
scores = []

while True:
    try:
        score_input = input("Enter score (or 'done'): ")
        if score_input.lower() == 'done':
            break
        score = int(score_input)
        if 0 <= score <= 100:
            scores.append(score)
        else:
            print("Score must be between 0-100")
    except ValueError:
        print("Please enter a valid number")

if scores:
    average = sum(scores) / len(scores)
    print(f"Average: {average:.2f}")
```

---

## Summary

| Statement | Purpose | Example |
|-----------|---------|---------|
| if | Execute if true | `if x > 0: print(x)` |
| elif | Alternative condition | `elif x < 0: print("negative")` |
| else | Default case | `else: print("zero")` |
| while | Loop while true | `while x > 0:` |
| for | Loop over sequence | `for i in range(5):` |
| break | Exit loop | `break` |
| continue | Skip iteration | `continue` |
| else (loop) | Execute if no break | `else: print("done")` |

---

**Next**: [Functions](functions.md)
