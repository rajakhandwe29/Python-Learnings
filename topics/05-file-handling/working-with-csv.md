# Working with CSV in Python

## Reading CSV Files

```python
import csv

# Basic reading
with open("data.csv", "r") as f:
    reader = csv.reader(f)
    for row in reader:
        print(row)

# With header
with open("data.csv", "r") as f:
    reader = csv.DictReader(f)
    for row in reader:
        print(row["name"], row["age"])

# Using csv module with fieldnames
data = [
    {"id": 1, "name": "Alice", "score": 85},
    {"id": 2, "name": "Bob", "score": 92}
]

with open("output.csv", "w", newline="") as f:
    writer = csv.DictWriter(f, fieldnames=["id", "name", "score"])
    writer.writeheader()
    writer.writerows(data)
```

## Writing CSV Files

```python
import csv

data = [
    ["id", "name", "score"],
    [1, "Alice", 85],
    [2, "Bob", 92],
    [3, "Charlie", 78]
]

with open("output.csv", "w", newline="") as f:
    writer = csv.writer(f)
    writer.writerows(data)

# Using pandas (recommended for large datasets)
import pandas as pd

df = pd.read_csv("data.csv")
df["score"] = df["score"].astype(int)
df.to_csv("modified.csv", index=False)
```

## Summary

| Feature | Module | Use Case |
|---------|--------|----------|
| **Simple CSV** | `csv` | Small datasets, low overhead |
| **DataFrames** | `pandas` | Large datasets, analysis |

---

**Next:** Learn error handling for robust code!
