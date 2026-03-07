# Python Async Programming

## Description
Master asynchronous programming in Python using asyncio, covering coroutines, tasks, and concurrent execution patterns.

## Basic Async
```python
import asyncio

async def fetch_data(url: str) -> dict:
    async with aiohttp.ClientSession() as session:
        async with session.get(url) as response:
            return await response.json()

async def main():
    data = await fetch_data("https://api.example.com/data")
    print(data)

asyncio.run(main())
```

## Concurrent Tasks
```python
async def process_all(urls: list[str]):
    tasks = [asyncio.create_task(fetch_data(url)) for url in urls]
    results = await asyncio.gather(*tasks, return_exceptions=True)
    return [r for r in results if not isinstance(r, Exception)]
```

## Async Context Manager
```python
class DatabasePool:
    async def __aenter__(self):
        self.pool = await create_pool(dsn="postgresql://...")
        return self.pool

    async def __aexit__(self, *exc):
        await self.pool.close()
```

## Semaphore for Rate Limiting
```python
semaphore = asyncio.Semaphore(10)

async def limited_fetch(url):
    async with semaphore:
        return await fetch_data(url)
```
