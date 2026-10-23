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
    ...

assert first_two([1,2,3]) == [1,2]
```

2. **Finite counter (generator)**

```python
def count_from(start, step, n):
    """Yield n numbers: start, start+step, ..."""
    ...

assert list(count_from(10, 2, 3)) == [10,12,14]
```

---

## Core

3. **Custom iterator class**

```python
class Countdown:
    """Iterates n, n-1, ..., 1"""
    ...

assert list(Countdown(3)) == [3,2,1]
```

4. **Chunked (generator)**

```python
def chunked(iterable, size):
    """
    Yield lists of up to 'size' items from iterable.
    Works for any iterable without materializing all of it.
    """
    ...

assert list(chunked(range(5), 2)) == [[0,1],[2,3],[4]]
```

5. **Windowed (overlap)**

```python
def windowed(iterable, k):
    """Yield rolling windows (as tuples) of size k. If not enough items, yield nothing."""
    ...

assert list(windowed([1,2,3,4], 3)) == [(1,2,3),(2,3,4)]
```

6. **Merge sorted streams**

```python
def merge_sorted(a, b):
    """
    Merge two ascending iterables like merge step of mergesort.
    Must be streaming (no full materialization).
    """
    ...

assert list(merge_sorted([1,4,7],[2,3,8])) == [1,2,3,4,7,8]
```

7. **Flatten nested iterables with `yield from`**

```python
def flatten(nested):
    """Flatten one level: e.g., [[1,2],[3],[4,5]] -> 1,2,3,4,5"""
    ...

assert list(flatten([[1,2],[3],[4,5]])) == [1,2,3,4,5]
```

8. **Peekable iterator (wrapper)**

```python
class Peekable:
    """Wrap an iterator to allow peek()."""
    ...

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
    ...

data = ["name,age","Ada,36","Bob, x", "Eve, 30"]
assert list(rows_from_csv(data))[:1] == [{"name":"Ada","age":"36"}]
```
