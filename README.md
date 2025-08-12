# Python-threads
codes used during projects
# Python Codex — Practical Patterns

A compact reference of production‑friendly Python patterns: dataclasses, pathlib, caching, context managers, generators, structured errors, CLI, logging, async, and testing.

## Features
- **Typed, minimal examples** you can drop into real code
- **Zero frameworks required** (standard library first)
- **Includes a Jupyter/VS Code demo** using `# %%` cells

## Quickstart
```bash
python -V            # Python 3.10+
python -m venv .venv && source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -U pip pytest
```

Optional extras for certain cells:
```bash
pip install aiohttp  # for the async HTTP example
```

## Examples
### Dataclass model
```python
from dataclasses import dataclass

@dataclass(slots=True, frozen=True)
class User:
    id: int
    email: str
```

### Files with `pathlib`
```python
from pathlib import Path
DATA = Path("data"); DATA.mkdir(exist_ok=True)
(DATA/"out.txt").write_text("hello\n", encoding="utf-8")
```

### Caching
```python
from functools import lru_cache
@lru_cache(maxsize=512)
def fib(n:int)->int: return n if n<2 else fib(n-1)+fib(n-2)
```

### CLI
```python
import argparse
p = argparse.ArgumentParser(prog="thumbs")
p.add_argument("path"); p.add_argument("--size", type=int, default=256)
args = p.parse_args()
print(f"making thumbnail for {args.path} at {args.size}px")
```

### Logging
```python
import logging
logging.basicConfig(level=logging.INFO,
    format="%(asctime)s %(levelname)s %(name)s: %(message)s")
log = logging.getLogger("worker")
log.info("started", extra={"job": 42})
```

### Testing
```python
# tests/test_math.py
import pytest
@pytest.mark.parametrize("a,b,ans", [(1,2,3),(0,0,0),(-1,1,0)])
def test_add(a,b,ans):
    assert a + b == ans
```

## Project Scaffold
```
my_tool/
  pyproject.toml
  my_tool/
    __init__.py
    cli.py
  tests/
    test_cli.py
```

## License
MIT — use freely.
