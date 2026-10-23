# Lambda, Map, Filter, Reduce — Exercises

**Goals:** write concise transformations, filter streams, fold aggregates with `reduce`, know when a comprehension is clearer, and compose pure functions.

---

## Warm-ups

1. **Normalize names (lambda + map)**

```python
def normalize_names(names):
    """Strip and Title Case each name; return list."""
    ...
assert normalize_names(["  ada ", "BOB"]) == ["Ada","Bob"]
```

2. **Keep even squares (filter + map)**

```python
def even_squares(xs):
    """Return list of x*x for even x in xs."""
    ...
assert even_squares([1,2,3,4]) == [4,16]
```

---

## Core

3. **Reduce: product**

```python
from functools import reduce
import operator as op

def product(xs):
    """Return multiplicative product of items; empty -> 1."""
    ...
assert product([2,3,4]) == 24
```

4. **Reduce: max by key**

```python
def max_by_key(items, key):
    """
    items: iterable; key: function.
    Return item with maximum key(item). Raise ValueError for empty.
    """
    ...

assert max_by_key(["aa","b","ccc"], len) == "ccc"
```

5. **Pipeline with lambdas**

```python
def pipeline(x, funcs):
    """Apply each f in funcs to x (left-to-right)."""
    ...

assert pipeline(2, [lambda x:x+3, lambda x:x*10]) == 50
```

6. **Word count (map + reduce)**

```python
def word_count(lines):
    """
    Split lines on whitespace; return dict word->count (lowercased).
    """
    ...

assert word_count(["Red red","blue"]) == {"red":2,"blue":1}
```

7. **Partition with filter**

```python
def partition(xs, pred):
    """Return (truthy_list, falsy_list)."""
    ...

pos, neg = partition([1,-2,3,0,-1], lambda x: x>0)
assert pos == [1,3] and neg == [-2,0,-1]
```

8. **When NOT to use reduce**
   Rewrite using a **comprehension** (clearer & faster in CPython for simple cases):

```python
def squares_comprehension(xs):
    """Return list of x*x for x in xs."""
    ...
assert squares_comprehension([1,2,3]) == [1,4,9]
```

---

## Challenge

9. **Mini query engine**

```python
def query(rows, *, select=lambda r: r, where=lambda r: True, order_by=None, limit=None):
    """
    rows: iterable of dicts.
    where: filter predicate on rows.
    select: mapping row->row' (e.g., pick fields or transform).
    order_by: key function or None.
    limit: int or None.
    Return list of transformed rows.
    """
    ...

rows = [{"name":"Ada","age":36},{"name":"Bob","age":20},{"name":"Eve","age":30}]
res = query(rows, where=lambda r:r["age"]>=30, select=lambda r: r["name"], order_by=None)
assert res == ["Ada","Eve"]
```
