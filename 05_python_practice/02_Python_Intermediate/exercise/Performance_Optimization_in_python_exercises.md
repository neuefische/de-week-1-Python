# Performance Optimization — Exercises

**Goals:** measure first (time and memory), then optimize: data structures, algorithmic complexity, generator pipelines, caching, and avoiding unnecessary work. Use stdlib tools: `time`, `timeit`, `functools.lru_cache`, and simple profiling.

> Keep solutions pure-Python unless told otherwise.

---

## Warm-ups

1. **Time a function (micro-benchmark)**

```python
import timeit

def slow_sum(n):
    s = 0
    for i in range(n):
        s += i
    return s

def time_ms(fn, *args, repeats=5, number=1):
    """Return average milliseconds over runs (timeit)."""
    stmt = lambda: fn(*args)
    t = timeit.timeit(stmt, number=repeats)
    return (t/repeats)*1000

ms = time_ms(slow_sum, 10000, repeats=5)
assert ms >= 0
```

2. **Choose the right container**

```python
def contains_all(haystack, needles):
    """
    Return True if every needle is in haystack.
    Optimize membership checks by converting haystack once if needed.
    """
    hs = set(haystack) if not isinstance(haystack, set) else haystack
    return all(n in hs for n in needles)

assert contains_all(range(1000), [10, 999]) is True
```

---

## Core

3. **Avoid repeated work**

```python
def dedupe_preserve_order(xs):
    """Remove duplicates while preserving order in O(n)."""
    seen, out = set(), []
    for x in xs:
        if x not in seen:
            seen.add(x); out.append(x)
    return out

assert dedupe_preserve_order([1,2,1,3,2,4,4]) == [1,2,3,4]
```

4. **Generator pipeline to control memory**

```python
def read_numbers(lines):
    """lines: iterable of strings; lazily yield ints, skipping invalid."""
    for ln in lines:
        ln = ln.strip()
        if not ln: 
            continue
        try:
            yield int(ln)
        except ValueError:
            continue

def sum_large_stream(lines):
    """Sum without materializing all numbers in memory."""
    return sum(read_numbers(lines))

assert sum_large_stream(["1","2","x","3"]) == 6
```

5. **Caching with LRU**

```python
from functools import lru_cache

@lru_cache(maxsize=256)
def fib(n):
    if n < 2: return n
    return fib(n-1) + fib(n-2)

assert fib(200) >= 0  # runs instantly with cache
```

6. **Batching to reduce overhead**

```python
def batched(iterable, size):
    """Yield lists of size 'size' except possibly last."""
    batch = []
    for x in iterable:
        batch.append(x)
        if len(batch) == size:
            yield batch; batch=[]
    if batch: 
        yield batch

def process_in_batches(xs, size):
    """Simulate heavy per-call overhead by working in batches."""
    total = 0
    for b in batched(xs, size):
        total += sum(b)
    return total

assert process_in_batches(range(10), 4) == sum(range(10))
```

7. **Algorithmic choice (n^2 → n log n)**

```python
def intersect_slow(a, b):
    return [x for x in a if x in b]  # O(n*m)

def intersect_fast(a, b):
    bs = set(b)
    return [x for x in a if x in bs]

A = list(range(1000)); B = list(range(500, 1500))
assert intersect_fast(A,B) == intersect_slow(A,B)
```

8. **String building (join > += in loops)**

```python
def join_numbers(n):
    return ",".join(str(i) for i in range(n))

s = join_numbers(5)
assert s == "0,1,2,3,4"
```

9. **Profile hotspot (guided)**

```python
def words_longer_than(text, k):
    return [w for w in text.split() if len(w) > k]

# Use %timeit in notebook to compare for different k and inputs.
```

---

## Challenge

10. **Top-K with heap (n log k)**

```python
import heapq

def top_k(nums, k):
    """
    Return k largest numbers from nums using a min-heap of size k.
    """
    it = iter(nums)
    heap = []
    for x in it:
        if len(heap) < k:
            heapq.heappush(heap, x)
        elif x > heap[0]:
            heapq.heapreplace(heap, x)
    return sorted(heap, reverse=True)

assert top_k([5,1,9,3,7,2,8], 3) == [9,8,7]
```

11. **Streaming group counts (memory-aware)**

```python
def group_counts(lines):
    """
    lines: iterable strings "group, value"
    Return dict group->count without storing all lines at once.
    Skip malformed lines.
    """
    counts = {}
    for ln in lines:
        try:
            g, _ = [x.strip() for x in ln.split(",", 1)]
        except ValueError:
            continue
        counts[g] = counts.get(g, 0) + 1
    return counts

assert group_counts(["A,1","B,2","A,3","bad"]) == {"A":2,"B":1}
```