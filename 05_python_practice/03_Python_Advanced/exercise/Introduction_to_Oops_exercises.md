
# Introduction to OOP — Exercises

**Goals:** model data with classes, use the Python data model, design for readability & correctness, and apply inheritance/composition thoughtfully.

> Format: Each task includes a starter signature and simple `assert` tests. Add more tests as you go.

---

## Warm-ups

1. **Point with distance and repr**

```python
import math
class Point:
    """
    Immutable 2D point.
    - attributes: x, y
    - methods: distance_to_origin() -> float
    - nice __repr__ like 'Point(x=1, y=2)'
    """
    ...

p = Point(3, 4)
assert p.distance_to_origin() == 5
assert "Point(" in repr(p)
```

2. **User as dataclass with validation**

```python
from dataclasses import dataclass

@dataclass
class User:
    """
    Fields: name (str), email (str)
    - normalize: strip spaces; email -> lowercase
    - property: domain (e.g., 'example.com')
    - __post_init__: validate that email contains exactly one '@' and a '.'
    """
    ...

u = User("  Ada Lovelace ", "ADA@EXAMPLE.COM ")
assert u.name == "Ada Lovelace" and u.domain == "example.com"
```

3. **Class variable: counting instances**

```python
class Counter:
    """Keep a class-level count of created instances in Counter.created."""
    created = 0
    def __init__(self):
        ...
c1, c2 = Counter(), Counter()
assert Counter.created == 2
```

---

## Core

4. **Vector2D with rich ops (immutable)**

```python
from dataclasses import dataclass

@dataclass(frozen=True, slots=True)
class Vector2D:
    """Support +, -, scalar *, equality, and hashing."""
    x: float
    y: float
    def __add__(self, other): ...
    def __sub__(self, other): ...
    def __mul__(self, scalar): ...
    def __rmul__(self, scalar): ...

v = Vector2D(1,2) + Vector2D(3,4)
assert v == Vector2D(4,6)
assert 2 * Vector2D(1,1) == Vector2D(2,2)
s = {Vector2D(0,0)}  # hashable
```

5. **Rectangle with computed properties**

```python
class Rectangle:
    """
    width >=0, height >=0
    - area (read-only property)
    - perimeter (read-only property)
    """
    ...
r = Rectangle(3,4)
assert r.area == 12 and r.perimeter == 14
```

6. **Abstract Shape hierarchy**

```python
from abc import ABC, abstractmethod
import math

class Shape(ABC):
    @abstractmethod
    def area(self) -> float: ...

class Circle(Shape):
    ...
class Rect(Shape):
    ...

assert round(Circle(1).area(), 5) == round(math.pi, 5)
assert Rect(2,3).area() == 6
```

7. **Composition: Order with LineItems**

```python
class LineItem:
    """name:str, qty:int>0, unit_price:float>=0; total()"""
    ...
class Order:
    """items: list[LineItem]; total() -> float"""
    ...
o = Order([LineItem("apple", 2, 1.5), LineItem("pear", 1, 2.0)])
assert o.total() == 5.0
```

8. **Context manager class**

```python
import time

class Timer:
    """
    with Timer() as t: ...; t.elapsed contains seconds (float)
    Implement __enter__/__exit__.
    """
    ...
with Timer() as t:
    for _ in range(10000): pass
assert isinstance(t.elapsed, float)
```

9. **Iterable/iterator protocol**

```python
class RangeInclusive:
    """Iterate from start to end inclusive."""
    def __init__(self, start, end): ...
    def __iter__(self): ...
    def __next__(self): ...
assert list(RangeInclusive(3,5)) == [3,4,5]
```

10. **Typing with Protocol**

```python
from typing import Protocol, Iterable

class Closable(Protocol):
    def close(self) -> None: ...

def close_all(resources: Iterable[Closable]) -> int:
    """Call .close() on each resource; return count."""
    ...
class R:
    def __init__(self): self.closed=False
    def close(self): self.closed=True
r = R()
assert close_all([r]) == 1 and r.closed is True
```

---

## Challenges

11. **LRU Cache (class)**

```python
from collections import OrderedDict

class LRUCache:
    """
    Capacity-bounded dict-like cache.
    - get(key, default=None)
    - set(key, value)
    - __contains__
    - evict least-recently-used on overflow
    """
    ...
c = LRUCache(2)
c.set("a",1); c.set("b",2); _ = c.get("a"); c.set("c",3)
assert "b" not in c and "a" in c and "c" in c
```

12. **Strategy pattern: discounts**

```python
from abc import ABC, abstractmethod

class Discount(ABC):
    @abstractmethod
    def apply(self, amount: float) -> float: ...

class NoDiscount(Discount): ...
class Percent(Discount): ...
class Flat(Discount): ...

def total_with_discount(amount, strategy: Discount) -> float:
    ...
assert total_with_discount(100, Percent(0.1)) == 90
assert total_with_discount(50, Flat(5)) == 45
```

> Notes: Prefer **composition** to inheritance unless you need polymorphism; prefer **dataclasses** for plain data; use `__slots__` for large numbers of instances to reduce memory.
