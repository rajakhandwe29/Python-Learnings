# File Operations in Python: A Comprehensive Guide

## Table of Contents
1. [Reading Files](#reading-files)
2. [Writing Files](#writing-files)
3. [File Modes](#file-modes)
4. [Context Managers](#context-managers)
5. [Working with Paths](#working-with-paths)
6. [Directory Operations](#directory-operations)
7. [Best Practices](#best-practices)
8. [Summary](#summary)

## Reading Files

### Read Entire File
```python
# Read all content at once
with open("file.txt", "r") as f:
    content = f.read()
print(content)

# Read into list of lines
with open("file.txt", "r") as f:
    lines = f.readlines()
for line in lines:
    print(line.strip())

# Read one line at a time
with open("file.txt", "r") as f:
    while True:
        line = f.readline()
        if not line:
            break
        print(line.strip())
```

### Iterate Over Lines
```python
# Memory efficient iteration
with open("large_file.txt", "r") as f:
    for line in f:
        print(line.strip())

# With line numbers
with open("file.txt", "r") as f:
    for i, line in enumerate(f, 1):
        print(f"{i}: {line.strip()}")
```

## Writing Files

### Write Content
```python
# Write string to file
with open("output.txt", "w") as f:
    f.write("Hello, World!\n")
    f.write("Second line\n")

# Write multiple lines
lines = ["Line 1", "Line 2", "Line 3"]
with open("output.txt", "w") as f:
    f.writelines(line + "\n" for line in lines)

# Append to file
with open("output.txt", "a") as f:
    f.write("Appended line\n")
```

## File Modes

```python
# Common modes:
# "r" - Read (default)
# "w" - Write (creates/truncates)
# "a" - Append
# "x" - Create (error if exists)
# "b" - Binary mode
# "t" - Text mode (default)
# "+" - Read and write

# Text read
with open("file.txt", "r") as f:
    content = f.read()

# Binary read
with open("image.png", "rb") as f:
    data = f.read()

# Read and write
with open("file.txt", "r+") as f:
    content = f.read()
    f.write("More content")
```

## Context Managers

```python
# Good - automatic file closing
with open("file.txt", "r") as f:
    content = f.read()

# Bad - manual file management
f = open("file.txt", "r")
try:
    content = f.read()
finally:
    f.close()

# Custom context manager
from contextlib import contextmanager

@contextmanager
def open_files(filenames):
    files = [open(f, "r") for f in filenames]
    try:
        yield files
    finally:
        for f in files:
            f.close()

# Usage
with open_files(["file1.txt", "file2.txt"]) as files:
    for f in files:
        print(f.read())
```

## Working with Paths

```python
from pathlib import Path

# Create path
p = Path("folder/file.txt")

# Path properties
print(p.exists())      # Check if exists
print(p.is_file())     # Is it a file?
print(p.is_dir())      # Is it a directory?
print(p.name)          # Filename
print(p.stem)          # Filename without extension
print(p.suffix)        # File extension
print(p.parent)        # Parent directory

# Path operations
new_path = p.with_stem("newfile")
print(new_path)  # Output: folder/newfile.txt

# Join paths
p = Path("folder") / "subfolder" / "file.txt"

# Read/write with Path
p.write_text("content")
content = p.read_text()

# List files
folder = Path(".")
for file in folder.glob("*.txt"):
    print(file)

# All files recursively
for file in folder.rglob("*.txt"):
    print(file)
```

## Directory Operations

```python
import os
from pathlib import Path

# Create directories
os.makedirs("folder/subfolder", exist_ok=True)

# List directory
files = os.listdir("folder")
print(files)

# Walk directory tree
for root, dirs, files in os.walk("folder"):
    for file in files:
        print(os.path.join(root, file))

# Delete files
os.remove("file.txt")
os.rmdir("empty_folder")
import shutil
shutil.rmtree("folder_with_contents")

# Rename
os.rename("old_name.txt", "new_name.txt")

# Get current directory
print(os.getcwd())

# Change directory
os.chdir("folder")
```

## Best Practices

### 1. Always Use Context Managers
```python
# GOOD
with open("file.txt", "r") as f:
    content = f.read()

# BAD - file not closed if exception occurs
f = open("file.txt", "r")
content = f.read()
f.close()
```

### 2. Use pathlib for Cross-Platform Paths
```python
from pathlib import Path

# GOOD - works on Windows and Unix
path = Path("data") / "file.txt"

# LESS GOOD - hardcoded separators
path = "data\\file.txt"  # Windows only
```

### 3. Handle Exceptions
```python
from pathlib import Path

try:
    content = Path("file.txt").read_text()
except FileNotFoundError:
    print("File not found")
except IOError:
    print("Cannot read file")
```

### 4. Use Appropriate Read Mode for Data
```python
# Text files
with open("text.txt", "r") as f:
    content = f.read()

# Binary files
with open("image.png", "rb") as f:
    data = f.read()

# Line by line iteration (memory efficient)
with open("large_file.txt", "r") as f:
    for line in f:
        process(line)
```

## Summary

| Operation | Method | Example |
|-----------|--------|---------|
| **Read all** | `f.read()` | Full content |
| **Read lines** | `f.readlines()` | List of lines |
| **Iterate** | `for line in f` | Memory efficient |
| **Write** | `f.write()` | Write string |
| **Append** | Open with "a" | Add to end |
| **Path ops** | `Path()` | Cross-platform |

### Key Takeaways

1. **Use context managers** - Ensures files are closed
2. **Pathlib over os.path** - More Pythonic and readable
3. **Handle exceptions** - Files might not exist
4. **Choose read mode carefully** - Text vs binary
5. **Iterate for large files** - Saves memory
6. **Encode/decode properly** - UTF-8 for text
7. **Test file operations** - Edge cases matter

---

**Next:** Learn error handling for robust applications.
