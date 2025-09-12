# Iterators & Generators — Exercises

**Goals:** understand the iterator protocol, build custom iterators, write generator functions, compose with `yield from`, and stream data efficiently.

---

## Warm-ups

1. **Manual iteration**

```python
def first_two(iterable):
    """
    Manually consume iterator with next(); return list of first two items (or fewer).
    """
    it = iter(iterable)
    out = []
    for _ in range(2):
        try:
            out.append(next(it))
        except StopIteration:
            break
    return out

assert first_two([1,2,3]) == [1,2]
```

2. **Finite counter (generator)**

```python
def count_from(start, step, n):
    """Yield n numbers: start, start+step, ..."""
    for i in range(n):
        yield start + i*step

assert list(count_from(10, 2, 3)) == [10,12,14]
```

---

## Core

3. **Custom iterator class**

```python
class Countdown:
    """Iterates n, n-1, ..., 1"""
    def __init__(self, n): 
        self.n = n
    def __iter__(self):
        return self
    def __next__(self):
        if self.n <= 0:
            raise StopIteration
        v = self.n
        self.n -= 1
        return v

assert list(Countdown(3)) == [3,2,1]
```

4. **Chunked (generator)**

```python
def chunked(iterable, size):
    """
    Yield lists of up to 'size' items from iterable.
    Works for any iterable without materializing all of it.
    """
    buf = []
    for x in iterable:
        buf.append(x)
        if len(buf) == size:
            yield buf; buf=[]
    if buf:
        yield buf

assert list(chunked(range(5), 2)) == [[0,1],[2,3],[4]]
```

5. **Windowed (overlap)**

```python
def windowed(iterable, k):
    """Yield rolling windows (as tuples) of size k. If not enough items, yield nothing."""
    it = iter(iterable)
    from collections import deque
    win = deque(maxlen=k)
    for x in it:
        win.append(x)
        if len(win) == k:
            yield tuple(win)

assert list(windowed([1,2,3,4], 3)) == [(1,2,3),(2,3,4)]
```

6. **Merge sorted streams**

```python
def merge_sorted(a, b):
    """
    Merge two ascending iterables like merge step of mergesort.
    Must be streaming (no full materialization).
    """
    a = iter(a); b = iter(b)
    try: x = next(a)
    except StopIteration: 
        yield from b; return
    try: y = next(b)
    except StopIteration:
        yield x; yield from a; return
    while True:
        if x <= y:
            yield x
            try: x = next(a)
            except StopIteration:
                yield y; yield from b; return
        else:
            yield y
            try: y = next(b)
            except StopIteration:
                yield x; yield from a; return

assert list(merge_sorted([1,4,7],[2,3,8])) == [1,2,3,4,7,8]
```

7. **Flatten nested iterables with `yield from`**

```python
def flatten(nested):
    """Flatten one level: e.g., [[1,2],[3],[4,5]] -> 1,2,3,4,5"""
    for part in nested:
        yield from part

assert list(flatten([[1,2],[3],[4,5]])) == [1,2,3,4,5]
```

8. **Peekable iterator (wrapper)**

```python
class Peekable:
    """Wrap an iterator to allow peek()."""
    _MISSING = object()
    def __init__(self, iterable):
        self._it = iter(iterable)
        self._buf = self._MISSING
    def peek(self):
        if self._buf is self._MISSING:
            try:
                self._buf = next(self._it)
            except StopIteration:
                return None
        return self._buf
    def __iter__(self): return self
    def __next__(self):
        if self._buf is not self._MISSING:
            v = self._buf; self._buf = self._MISSING; return v
        return next(self._it)

p = Peekable([1,2]); assert p.peek()==1 and next(p)==1 and next(p)==2
```

---

## Challenge

9. **CSV stream → dicts, robust & lazy**

```python
def rows_from_csv(lines, delimiter=","):
    """
    lines: iterable of strings 'a,b,c'
    First line = header. Yield dict rows lazily.
    Skip malformed rows (different number of fields).
    """
    it = iter(lines)
    try:
        header = next(it).strip().split(delimiter)
    except StopIteration:
        return
    for line in it:
        parts = [p.strip() for p in line.split(delimiter)]
        if len(parts) != len(header):
            continue
        yield dict(zip(header, parts))

data = ["name,age","Ada,36","Bob, x", "Eve, 30"]
assert list(rows_from_csv(data))[:1] == [{"name":"Ada","age":"36"}]
```
