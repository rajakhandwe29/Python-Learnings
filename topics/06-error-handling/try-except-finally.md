# Try-Except-Finally in Python

## Complete Error Handling Pattern

```python
# Standard error handling pattern
try:
    # Code that might raise exception
    data = risky_operation()
    process_data(data)
except SpecificException as e:
    # Handle specific error
    log_error(e)
    handle_error()
except AnotherException as e:
    # Handle another error
    notify_user(e)
except Exception as e:
    # Fallback for unexpected errors
    print(f"Unexpected error: {e}")
else:
    # Executes if no exception
    print("Operation successful")
    return result
finally:
    # Always executes
    cleanup_resources()
```

## File Operations Example

```python
# Safe file reading
def read_file_safely(filename):
    try:
        with open(filename, "r") as f:
            return f.read()
    except FileNotFoundError:
        print(f"File {filename} not found")
        return None
    except IOError as e:
        print(f"IO error: {e}")
        return None
    finally:
        print("Read operation completed")

# Safe file writing
def write_file_safely(filename, content):
    try:
        with open(filename, "w") as f:
            f.write(content)
        print(f"Successfully wrote to {filename}")
    except IOError as e:
        print(f"Cannot write to {filename}: {e}")
    finally:
        print("Write operation completed")
```

## Database Operations Example

```python
def get_user_from_database(user_id):
    connection = None
    try:
        connection = create_database_connection()
        result = connection.query(f"SELECT * FROM users WHERE id = {user_id}")
        return result
    except ConnectionError:
        print("Database connection failed")
        return None
    except QueryError as e:
        print(f"Query failed: {e}")
        return None
    finally:
        if connection:
            connection.close()
```

## Best Practices

1. **Specific exceptions first** - More specific before general
2. **Use finally for cleanup** - Files, connections, resources
3. **Don't silence errors** - Always log or re-raise
4. **Use context managers** - Automatic resource management
5. **Test both paths** - Success and failure

---

**Next:** Create custom exceptions for specific errors!
