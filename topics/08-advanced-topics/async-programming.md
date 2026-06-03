# Async Programming in Python

## Async/Await Basics

```python
import asyncio

async def fetch_data(url, delay):
    """Simulate network request"""
    await asyncio.sleep(delay)
    return f"Data from {url}"

async def main():
    result = await fetch_data("example.com", 2)
    print(result)

asyncio.run(main())
```

## Concurrent Tasks

```python
import asyncio

async def task(name, delay):
    print(f"{name} starting")
    await asyncio.sleep(delay)
    print(f"{name} done")
    return f"Result from {name}"

async def main():
    # Create tasks
    tasks = [
        task("Task-1", 2),
        task("Task-2", 1),
        task("Task-3", 1.5),
    ]
    
    # Run concurrently
    results = await asyncio.gather(*tasks)
    print(results)

asyncio.run(main())
```

## HTTP Requests

```python
import asyncio
import aiohttp

async def fetch(url):
    async with aiohttp.ClientSession() as session:
        async with session.get(url) as response:
            return await response.text()

async def main():
    urls = [
        "https://example.com",
        "https://example.org",
        "https://example.net",
    ]
    tasks = [fetch(url) for url in urls]
    results = await asyncio.gather(*tasks)
    print(f"Fetched {len(results)} URLs")

asyncio.run(main())
```

## Async Patterns

```python
# Consumer/Producer
async def producer(queue):
    for i in range(5):
        await queue.put(i)
    await queue.put(None)  # Signal end

async def consumer(queue):
    while True:
        item = await queue.get()
        if item is None:
            break
        print(f"Processing {item}")

async def main():
    queue = asyncio.Queue()
    await asyncio.gather(
        producer(queue),
        consumer(queue),
    )

asyncio.run(main())
```

## Best Practices

1. **Use async for I/O** - Not CPU-bound work
2. **Gather tasks** - Run concurrently
3. **Handle timeouts** - Prevent hanging
4. **Use context managers** - For cleanup
5. **Test thoroughly** - Concurrency issues are complex

---

**Next:** Testing and performance!
