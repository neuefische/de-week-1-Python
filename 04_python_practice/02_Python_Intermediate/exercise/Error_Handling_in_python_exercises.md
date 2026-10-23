# Error Handling — Exercises

**Goals:** write defensive code with `try/except/else/finally`, validate inputs, raise custom exceptions, use exception chaining, and manage resources with context managers.

> Format: Each task gives a starter signature and quick tests (you can adapt to cells).

---

## Warm-ups

1. **Safe int**

```python
def to_int(s, default=None):
    """Return int(s) after strip; return default on ValueError/TypeError."""
    ...

assert to_int(" 42 ") == 42
assert to_int("x", default=-1) == -1
```

2. **Divide with cleanup**

```python
def safe_div(a, b, default=None, *, on_error="log"):
    """
    Return a/b. On ZeroDivisionError or TypeError return default.
    If on_error == 'raise', re-raise instead of default.
    """
    ...

assert safe_div(6,3) == 2
assert safe_div(1,0, default=float('inf')) == float('inf')
```

---

## Core

3. **Custom exception + validation**

```python
class BadRecordError(ValueError):
    """Raised when a data record is invalid."""

def parse_record(line):
    """
    'name,age' -> {'name':str, 'age':int}
    - age must be 0..120
    - raise BadRecordError with informative message on failure
    """
    ...

assert parse_record("Ada, 36") == {"name":"Ada","age":36}
```

4. **Bulk parse with error collection**

```python
def parse_many(lines):
    """
    Return (ok_list, errors_list).
    errors_list contains tuples: (line, exc)
    """
    ...

ok, errs = parse_many(["Ada,36","Bob,200","bad"])
assert len(ok)==1 and len(errs)==2
```

5. **Exception chaining (wrapping)**

```python
def load_config(env):
    """
    Simulate reading a config dict for env.
    - raise FileNotFoundError if env == 'missing'
    """
    if env == "missing":
        raise FileNotFoundError("config missing")
    return {"env": env, "retries": 3}

class ConfigLoadError(RuntimeError): pass

def init_app(env):
    """
    Wrap load_config errors as ConfigLoadError using 'raise ... from ...'
    """
    ...

assert "App" in init_app("prod")
try:
    init_app("missing")
except ConfigLoadError as e:
    assert e.__cause__ is not None
```

6. **Context manager (file safety)**

```python
from contextlib import contextmanager

@contextmanager
def opened(path, mode="r", encoding="utf-8"):
    """
    Open a file safely and always close it.
    Re-raise exceptions unchanged.
    """
    ...

# usage example (create temp file in notebook working dir):
with opened("tmp.txt","w") as f:
    f.write("hello")
with opened("tmp.txt") as f:
    assert f.read() == "hello"
```

---

## Challenge

7. **Retry with backoff**

```python
import time

def retry(fn, *, attempts=3, delay=0.0, backoff=1.0, exceptions=(Exception,)):
    """
    Call fn(); on exception, sleep 'delay', then multiply delay by 'backoff',
    and retry, up to 'attempts' times. Re-raise last error on failure.
    """
    ...

# test
n={"x":0}
def flaky():
    n["x"]+=1
    if n["x"]<2: 
        raise RuntimeError("boom")
    return "ok"

assert retry(flaky, attempts=3) == "ok"
```

