# Lambda, Map, Filter, Reduce — Exercises

**Goals:** write concise transformations, filter streams, fold aggregates with `reduce`, know when a comprehension is clearer, and compose pure functions.

---

## Warm-ups

1. **Normalize names (lambda + map)**

```python
def normalize_names(names):
    """Strip and Title Case each name; return list."""
    return list(map(lambda s: s.strip().title(), names))

assert normalize_names(["  ada ", "BOB"]) == ["Ada","Bob"]
```

2. **Keep even squares (filter + map)**

```python
def even_squares(xs):
    return list(map(lambda x: x*x, filter(lambda x: x%2==0, xs)))

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
    return reduce(op.mul, xs, 1)

assert product([2,3,4]) == 24
```

4. **Reduce: max by key**

```python
def max_by_key(items, key):
    """
    items: iterable; key: function.
    Return item with maximum key(item). Raise ValueError for empty.
    """
    from functools import reduce
    def pick(a, b): 
        return a if key(a) >= key(b) else b
    try:
        it = iter(items)
        first = next(it)
    except StopIteration:
        raise ValueError("empty")
    return reduce(pick, it, first)

assert max_by_key(["aa","b","ccc"], len) == "ccc"
```

5. **Pipeline with lambdas**

```python
def pipeline(x, funcs):
    """Apply each f in funcs to x (left-to-right)."""
    from functools import reduce
    return reduce(lambda v,f: f(v), funcs, x)

assert pipeline(2, [lambda x:x+3, lambda x:x*10]) == 50
```

6. **Word count (map + reduce)**

```python
def word_count(lines):
    """
    Split lines on whitespace; return dict word->count (lowercased).
    """
    from functools import reduce
    words = (w.lower() for line in lines for w in line.split())
    def add(d, w):
        d[w] = d.get(w,0)+1
        return d
    return reduce(add, words, {})

assert word_count(["Red red","blue"]) == {"red":2,"blue":1}
```

7. **Partition with filter**

```python
def partition(xs, pred):
    """Return (truthy_list, falsy_list)."""
    t = list(filter(pred, xs))
    f = list(filter(lambda x: not pred(x), xs))
    return t, f

pos, neg = partition([1,-2,3,0,-1], lambda x: x>0)
assert pos == [1,3] and neg == [-2,0,-1]
```

8. **When NOT to use reduce**
   Rewrite using a **comprehension** (clearer & faster in CPython for simple cases):

```python
def squares_comprehension(xs):
    return [x*x for x in xs]

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
    it = filter(where, rows)
    it = map(select, it)
    if order_by is not None:
        it = sorted(it, key=order_by)
    if limit is not None:
        out = []
        for i, r in enumerate(it):
            if i>=limit: break
            out.append(r)
        return out
    return list(it)

rows = [{"name":"Ada","age":36},{"name":"Bob","age":20},{"name":"Eve","age":30}]
res = query(rows, where=lambda r:r["age"]>=30, select=lambda r: r["name"], order_by=None)
assert res == ["Ada","Eve"]
```
