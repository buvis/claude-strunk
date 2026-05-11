# Package Organization and Tooling

## Naming Conventions (PEP 8)

| Kind | Convention | Example |
|------|------------|---------|
| Module / script file | `snake_case.py` | `data_loader.py`, `cli_runner.py` |
| Package directory | `lowercase` (avoid underscores) | `mypackage/`, `utils/` |
| Class | `CapWords` | `HttpClient`, `UserRepository` |
| Function / method / variable | `snake_case` | `parse_config`, `retry_count` |
| Constant | `UPPER_SNAKE_CASE` | `MAX_RETRIES`, `DEFAULT_TIMEOUT` |
| Type variable | `CapWords`, short | `T`, `KT`, `UserT` |
| "Internal" name | leading underscore | `_helper`, `_cache` |
| "Name-mangled" attr | double leading underscore | `__private` |
| Dunder | double leading + trailing | `__init__`, `__repr__` |

Never use kebab-case for `.py` files - `my-script.py` is not importable (`import my-script` is a syntax error). Use `my_script.py`. The only place kebab-case belongs in a Python project is the distribution name in `pyproject.toml` (`name = "my-package"`) and the CLI entry-point command itself (`my-tool`), both of which map to a `my_package` / `my_tool` importable module.

## Standard Project Layout

```
myproject/
├── src/
│   └── mypackage/
│       ├── __init__.py
│       ├── main.py
│       ├── api/
│       │   ├── __init__.py
│       │   └── routes.py
│       ├── models/
│       │   ├── __init__.py
│       │   └── user.py
│       └── utils/
│           ├── __init__.py
│           └── helpers.py
├── tests/
│   ├── __init__.py
│   ├── conftest.py
│   ├── test_api.py
│   └── test_models.py
├── pyproject.toml
├── README.md
└── .gitignore
```

## Import Conventions

```python
# Good: Import order - stdlib, third-party, local
import os
import sys
from pathlib import Path

import requests
from fastapi import FastAPI

from mypackage.models import User
from mypackage.utils import format_name

# Good: Use isort for automatic import sorting
# pip install isort
```

## __init__.py for Package Exports

```python
# mypackage/__init__.py
"""mypackage - A sample Python package."""

__version__ = "1.0.0"

# Export main classes/functions at package level
from mypackage.models import User, Post
from mypackage.utils import format_name

__all__ = ["User", "Post", "format_name"]
```

## Essential Commands

```bash
# Code formatting
black .
isort .

# Linting
ruff check .
pylint mypackage/

# Type checking
mypy .

# Testing
pytest --cov=mypackage --cov-report=html

# Security scanning
bandit -r .

# Dependency management
pip-audit
safety check
```

## pyproject.toml Configuration

```toml
[project]
name = "mypackage"
version = "1.0.0"
requires-python = ">=3.9"
dependencies = [
    "requests>=2.31.0",
    "pydantic>=2.0.0",
]

[project.optional-dependencies]
dev = [
    "pytest>=7.4.0",
    "pytest-cov>=4.1.0",
    "black>=23.0.0",
    "ruff>=0.1.0",
    "mypy>=1.5.0",
]

[tool.black]
line-length = 88
target-version = ['py39']

[tool.ruff]
line-length = 88
select = ["E", "F", "I", "N", "W"]

[tool.mypy]
python_version = "3.9"
warn_return_any = true
warn_unused_configs = true
disallow_untyped_defs = true

[tool.pytest.ini_options]
testpaths = ["tests"]
addopts = "--cov=mypackage --cov-report=term-missing"
```
