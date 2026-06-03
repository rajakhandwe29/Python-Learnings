# Multithreading in Python

## Basic Threading

```python
import threading
import time

def worker(name, delay):
    time.sleep(delay)
    print(f"{name} finished")

# Create thread
thread = threading.Thread(target=worker, args=("Thread-1", 2))
thread.start()
thread.join()  # Wait for completion

# Multiple threads
threads = []
for i in range(3):
    t = threading.Thread(target=worker, args=(f"Thread-{i}", 1))
    threads.append(t)
    t.start()

for t in threads:
    t.join()
```

## Thread Safety

```python
import threading

class Counter:
    def __init__(self):
        self.count = 0
        self.lock = threading.Lock()
    
    def increment(self):
        with self.lock:
            self.count += 1
    
    def get_count(self):
        with self.lock:
            return self.count

# Usage
counter = Counter()

def increment_many():
    for _ in range(1000):
        counter.increment()

threads = [threading.Thread(target=increment_many) for _ in range(5)]
for t in threads:
    t.start()
for t in threads:
    t.join()

print(counter.get_count())  # 5000
```

## Race Conditions

```python
# WRONG: Race condition
count = 0

def unsafe_increment():
    global count
    count += 1  # Not atomic!

# RIGHT: Use lock
lock = threading.Lock()

def safe_increment():
    global count
    with lock:
        count += 1
```

## Synchronization

```python
# Event - signal threads
event = threading.Event()

def waiter():
    print("Waiting...")
    event.wait()
    print("Event triggered!")

t = threading.Thread(target=waiter)
t.start()
time.sleep(2)
event.set()
t.join()

# Semaphore - limit access
semaphore = threading.Semaphore(2)

def limited_resource():
    with semaphore:
        print("Using resource")
        time.sleep(1)
```

## Best Practices

1. **Use locks** - Protect shared data
2. **Avoid deadlocks** - Consistent lock order
3. **Keep critical sections small**
4. **Use threading.Event** - For synchronization
5. **Test concurrency** - Race conditions are subtle

---

**Next:** Learn async programming!
