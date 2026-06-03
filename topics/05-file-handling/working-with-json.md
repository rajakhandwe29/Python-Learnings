# Working with JSON in Python

## Introduction

JSON (JavaScript Object Notation) is a lightweight data format widely used for APIs and configuration files. Python's `json` module makes JSON handling seamless.

## Basic JSON Operations

```python
import json

# Python to JSON (JSON serialization)
data = {"name": "Alice", "age": 30, "active": True}
json_string = json.dumps(data)
print(json_string)
# Output: {"name": "Alice", "age": 30, "active": true}

# JSON to Python (JSON deserialization)
json_data = '{"name": "Bob", "age": 25}'
python_dict = json.loads(json_data)
print(python_dict)  # Output: {'name': 'Bob', 'age': 25}
```

## File Operations

```python
import json

data = {
    "users": [
        {"id": 1, "name": "Alice", "email": "alice@example.com"},
        {"id": 2, "name": "Bob", "email": "bob@example.com"}
    ],
    "total": 2
}

# Write to file
with open("data.json", "w") as f:
    json.dump(data, f, indent=2)

# Read from file
with open("data.json", "r") as f:
    loaded_data = json.load(f)

print(loaded_data["users"][0]["name"])  # Output: Alice
```

## JSON vs Python Types

```python
# Python to JSON type mapping:
# dict -> object
# list -> array
# tuple -> array
# str -> string
# int/float -> number
# True/False -> true/false
# None -> null

# Example conversion
python_data = {
    "string": "hello",
    "number": 42,
    "float": 3.14,
    "boolean": True,
    "null_value": None,
    "list": [1, 2, 3],
    "nested": {"key": "value"}
}

json_string = json.dumps(python_data, indent=2)
print(json_string)

# Reconstructing
restored = json.loads(json_string)
print(restored["boolean"])  # Output: True
print(restored["null_value"])  # Output: None
```

## Pretty Printing

```python
import json

data = {"name": "Alice", "scores": [85, 90, 88], "active": True}

# Compact
print(json.dumps(data))
# Output: {"name": "Alice", "scores": [85, 90, 88], "active": true}

# Pretty printed with indentation
print(json.dumps(data, indent=2))
# Output:
# {
#   "name": "Alice",
#   "scores": [
#     85,
#     90,
#     88
#   ],
#   "active": true
# }

# Sorted keys
print(json.dumps(data, indent=2, sort_keys=True))
```

## Custom JSON Encoding/Decoding

```python
import json
from datetime import datetime

# Custom encoder
class DateTimeEncoder(json.JSONEncoder):
    def default(self, obj):
        if isinstance(obj, datetime):
            return obj.isoformat()
        return super().default(obj)

data = {
    "name": "Alice",
    "created": datetime.now()
}

json_string = json.dumps(data, cls=DateTimeEncoder, indent=2)
print(json_string)

# Custom decoder
def datetime_parser(dct):
    for key, value in dct.items():
        if isinstance(value, str) and 'T' in value:
            try:
                dct[key] = datetime.fromisoformat(value)
            except:
                pass
    return dct

loaded = json.loads(json_string, object_hook=datetime_parser)
print(loaded["created"])
```

## Practical Example: API Response

```python
import json
import requests

# Simulate API response
api_response = '''
{
    "status": "success",
    "data": {
        "users": [
            {"id": 1, "name": "Alice", "role": "admin"},
            {"id": 2, "name": "Bob", "role": "user"}
        ]
    }
}
'''

# Parse and process
response = json.loads(api_response)

if response["status"] == "success":
    for user in response["data"]["users"]:
        print(f"{user['name']} ({user['role']})")
```

## Error Handling

```python
import json

# JSONDecodeError for invalid JSON
try:
    invalid_json = '{"name": "Alice", "age": 30,}'  # Trailing comma
    data = json.loads(invalid_json)
except json.JSONDecodeError as e:
    print(f"Invalid JSON: {e}")

# TypeError for non-serializable objects
try:
    data = {"date": datetime.now()}
    json.dumps(data)
except TypeError as e:
    print(f"Cannot serialize: {e}")
```

## Best Practices

1. **Always use indent for readability** - Pretty print when human-readable
2. **Handle errors appropriately** - Validate JSON structure
3. **Use type hints** - Document expected JSON structure
4. **Validate after deserializing** - Check required fields
5. **Use custom encoders** - For complex types

---

**Next:** Learn CSV file handling for tabular data.
