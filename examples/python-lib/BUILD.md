# Python Library Build & Run Commands

## Prerequisites

- Python 3.10+
- [uv](https://docs.astral.sh/uv/) (recommended) or pip

```bash
# Install uv
curl -LsSf https://astral.sh/uv/install.sh | sh
```

## Quick Reference

```bash
uv sync                    # Install dependencies
uv run pytest              # Run tests
uv run pytest --cov        # Run tests with coverage
uv run ruff check .        # Lint
uv run ruff format .       # Format
uv run mypy src            # Type check
uv build                   # Build package
```

## Additional Commands

See `pyproject.toml` for full configuration. Common operations:

```bash
# Add dependencies
uv add requests pydantic
uv add --dev pytest mypy ruff

# Run specific tests
uv run pytest tests/test_api.py -v
uv run pytest -k "test_create"

# Publish
uv publish
```

## Common Issues

| Issue | Fix |
|-------|-----|
| `ModuleNotFoundError` | Run `uv sync` |
| mypy errors in tests | Add `[[tool.mypy.overrides]]` for tests in pyproject.toml |
| Import order failures | Run `uv run ruff check . --select I --fix` |

---

## Change Log

| Date | Change | Rationale |
|------|--------|-----------|
| [Date] | Initial build setup | Project setup |
