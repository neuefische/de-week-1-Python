# Concurrency & Parallelism — Exercises

**Goals:** pick the right model (threads/processes/async), write thread-safe code, stream through queues, use executors, design async pipelines, and handle cancellation/timeouts.

> **Safety notes**
>
> * For CPU-bound work, prefer **processes** (bypass GIL); for I/O-bound, prefer **threads** or **asyncio**.
> * When using `multiprocessing` or `ProcessPoolExecutor` on Windows/macOS, protect entry with:
>
>   ```python
>   if __name__ == "__main__":
>       ...
>   ```

---

## Warm-ups

1. **Thread-safe counter**

```python
import threading

class SafeCounter:
    """Increment from multiple threads safely using a Lock."""
    def __init__(self): ...
    def inc(self, n=1): ...
    @property
    def value(self): ...

cnt = SafeCounter()
def worker():
    for _ in range(1000): cnt.inc()
threads = [threading.Thread(target=worker) for _ in range(5)]
[t.start() for t in threads]; [t.join() for t in threads]
assert cnt.value == 5000
```

2. **Order-preserving ThreadPool**

```python
from concurrent.futures import ThreadPoolExecutor

def square(x): return x*x

def map_threaded(fn, xs, max_workers=4):
    """
    Map fn over xs using threads, preserving input order in the result.
    """
    ...
assert map_threaded(square, [1,2,3]) == [1,4,9]
```

---

## Core

3. **Producer/consumer with Queue**

```python
import threading, queue

def pipeline(nums):
    """
    Use a Queue to send nums to a worker thread that squares them.
    Use a sentinel (None) to signal completion.
    Return the collected results (preserve order if you wish).
    """
    ...
res = pipeline([1,2,3,4])
assert sorted(res) == [1,4,9,16]
```

4. **Process pool for CPU-bound work**

```python
from concurrent.futures import ProcessPoolExecutor

def is_prime(n: int) -> bool:
    """Trial division primality test (simple)."""
    ...

def primes_count(nums):
    """Count primes in nums using a ProcessPoolExecutor."""
    ...
assert primes_count([2,3,4,5,15,17,19]) == 5
```

5. **Async I/O with semaphore (limit concurrency)**

```python
import asyncio, random

async def fetch_one(i: int):
    """Simulate I/O by sleeping random small time, then return i."""
    await asyncio.sleep(0.01 + random.random()*0.02)
    return i

async def gather_limited(n, limit):
    """
    Schedule fetch_one for 0..n-1 but ensure at most 'limit' concurrent tasks
    using an asyncio.Semaphore.
    Return list of results (0..n-1) in any order.
    """
    ...
out = asyncio.run(gather_limited(10, 3))
assert sorted(out) == list(range(10))
```

6. **Cancellation & cleanup**

```python
import asyncio

async def sleepy():
    try:
        await asyncio.sleep(1)
        return "done"
    finally:
        # ensure cleanup code runs on cancel
        ...
async def cancel_demo():
    task = asyncio.create_task(sleepy())
    await asyncio.sleep(0.05)
    task.cancel()
    try:
        await task
    except asyncio.CancelledError:
        return "cancelled"

assert asyncio.run(cancel_demo()) == "cancelled"
```

7. **gather with return\_exceptions**

```python
import asyncio

async def ok(): return 1
async def boom(): raise RuntimeError("x")

async def run_mixed():
    """
    Use asyncio.gather(..., return_exceptions=True) so that errors become results.
    Return a list of results/exceptions.
    """
    ...
res = asyncio.run(run_mixed())
assert any(isinstance(x, RuntimeError) for x in res) and 1 in res
```

8. **Timeouts**

```python
import asyncio

async def maybe_slow(dt):
    await asyncio.sleep(dt); return dt

async def with_timeout(dt, timeout):
    """Run maybe_slow(dt) with asyncio.wait_for(..., timeout=timeout)."""
    ...
ok = asyncio.run(with_timeout(0.01, 0.1))
assert ok == 0.01
try:
    asyncio.run(with_timeout(0.2, 0.05))
    assert False, "should timeout"
except asyncio.TimeoutError:
    pass
```

9. **Mixing threads with async (offload CPU)**

```python
import asyncio

def cpu_heavy(n):
    """Return sum(i*i for i in range(n)) (CPU-bound)."""
    ...
async def compute_off_thread(n):
    """
    Use asyncio.to_thread(...) (3.9+) to offload cpu_heavy to a thread
    without blocking the event loop. Return the result.
    """
    ...
assert asyncio.run(compute_off_thread(10_000)) == sum(i*i for i in range(10_000))
```

---

## Challenges

10. **Ordered concurrent map with configurable backend**

```python
from concurrent.futures import ThreadPoolExecutor, ProcessPoolExecutor
from typing import Iterable, Callable, Literal

def concurrent_map(fn: Callable, xs: Iterable, *, backend: Literal["thread","process"]="thread", max_workers: int | None = None):
    """
    Apply fn to each x in xs concurrently and return results in input order.
    - backend='thread' uses ThreadPoolExecutor
    - backend='process' uses ProcessPoolExecutor
    """
    ...
assert concurrent_map(lambda x:x+1, [0,1,2], backend="thread") == [1,2,3]
assert concurrent_map(lambda x:x*x, [2,3,4], backend="process") == [4,9,16]
```

11. **Async rate-limited fetcher**

```python
import asyncio, time

async def rate_limited(ids, *, per_second=5):
    """
    Yield ids but enforce an average rate limit of 'per_second'.
    Use a simple token bucket (Semaphore/time) or sleep-based pacing.
    """
    ...
async def test_rate():
    started = time.perf_counter()
    out = [i async for i in rate_limited(range(10), per_second=10)]
    elapsed = time.perf_counter() - started
    assert out == list(range(10))
    assert elapsed >= 1.0/10 * 9 * 0.8  # loose lower bound
asyncio.run(test_rate())
```

12. **Async pipeline: parse → transform → aggregate**

```python
import asyncio

async def parse(line: str) -> dict | None:
    """Parse 'key:value' lines; return {'key': key, 'value': int(value)} or None."""
    ...
async def transform(rec: dict) -> dict:
    """Return rec with value doubled (simulate I/O with small sleep)."""
    ...
async def aggregate(lines: list[str]) -> dict[str, int]:
    """
    Use asyncio tasks + Semaphore to fan out parse/transform and then
    aggregate totals per key. Return dict key->total.
    """
    ...
res = asyncio.run(aggregate(["a:1","b:2","bad", "a:3"]))
assert res == {"a":8, "b":4}
```
