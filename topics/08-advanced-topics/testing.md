# Testing in Python

## Unit Testing

```python
import unittest

def add(a, b):
    return a + b

class TestMath(unittest.TestCase):
    def test_add(self):
        self.assertEqual(add(2, 3), 5)
    
    def test_add_negative(self):
        self.assertEqual(add(-1, -2), -3)
    
    def test_add_zero(self):
        self.assertEqual(add(0, 5), 5)

if __name__ == "__main__":
    unittest.main()
```

## Pytest

```python
# test_math.py
def add(a, b):
    return a + b

def test_add():
    assert add(2, 3) == 5

def test_add_negative():
    assert add(-1, -2) == -3

def test_add_zero():
    assert add(0, 5) == 5

# Run: pytest test_math.py
```

## Mocking

```python
from unittest.mock import Mock, patch

def get_user(user_id):
    # Calls external API
    response = requests.get(f"/api/users/{user_id}")
    return response.json()

def test_get_user():
    with patch("requests.get") as mock_get:
        mock_get.return_value.json.return_value = {"id": 1, "name": "Alice"}
        user = get_user(1)
        assert user["name"] == "Alice"
```

## Fixtures

```python
import pytest

@pytest.fixture
def db():
    database = create_db()
    yield database
    database.cleanup()

def test_insert(db):
    db.insert("users", {"name": "Alice"})
    assert len(db.query("users")) == 1
```

## Test Organization

```
project/
├── src/
│   └── app.py
└── tests/
    ├── test_app.py
    ├── conftest.py
    └── fixtures/
```

## Best Practices

1. **Test one thing** - Keep tests focused
2. **Use descriptive names** - Clear intent
3. **Test edge cases** - Null, empty, etc.
4. **Mock external dependencies** - Isolation
5. **Use fixtures** - DRY test setup

---

**Next:** Performance optimization!
