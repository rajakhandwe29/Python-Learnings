# File Handling in Python

## Overview

File handling is essential for working with data, configuration, and logging. Python provides powerful tools for reading, writing, and manipulating files.

## Quick Reference

### Read Files
```python
# Text file
with open("file.txt", "r") as f:
    content = f.read()

# Large file (memory efficient)
with open("file.txt", "r") as f:
    for line in f:
        process(line)

# JSON
import json
with open("data.json", "r") as f:
    data = json.load(f)

# CSV
import csv
with open("data.csv", "r") as f:
    reader = csv.DictReader(f)
    for row in reader:
        print(row)
```

### Write Files
```python
# Text file
with open("file.txt", "w") as f:
    f.write("content")

# JSON
import json
with open("data.json", "w") as f:
    json.dump(data, f)

# CSV
import csv
with open("data.csv", "w") as f:
    writer = csv.DictWriter(f, fieldnames=["col1", "col2"])
    writer.writerows(data)
```

## Key Concepts

1. **Context managers** - Automatic file closing
2. **Pathlib** - Cross-platform path operations
3. **Binary vs text** - Choose appropriate mode
4. **Error handling** - FileNotFoundError, IOError
5. **Encoding** - UTF-8 for text files
6. **Performance** - Use iteration for large files

## Topics Covered

- **File Operations** - Reading, writing, and path handling
- **JSON** - Working with JSON data
- **CSV** - Working with tabular data

---

**Next:** Master error handling for robust applications!
