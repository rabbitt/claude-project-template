# Django Coding Conventions

## Style Guide

We follow [PEP 8](https://peps.python.org/pep-0008/) and Django's own conventions, enforced by tooling.

## Tool Configuration

| Tool | Purpose | Config Location |
|------|---------|-----------------|
| ruff | Linting + formatting | `pyproject.toml` [tool.ruff] |
| mypy | Type checking | `pyproject.toml` [tool.mypy] |
| django-stubs | Django type hints | `pyproject.toml` [tool.django-stubs] |
| pytest-django | Testing | `pyproject.toml` [tool.pytest] |

**Check the config files** - they ARE the conventions. The AI should read `pyproject.toml` to understand project-specific rules.

**Before committing:**
```bash
ruff check . && ruff format --check . && mypy .
```

## Django-Specific Patterns

These aren't in PEP 8 but are Django conventions:

| Type | Pattern | Example |
|------|---------|---------|
| Model | `PascalCase`, singular | `User`, `OrderItem` |
| View class | `PascalCase` + `View` | `UserDetailView` |
| Serializer | `PascalCase` + `Serializer` | `UserSerializer` |
| Form | `PascalCase` + `Form` | `UserRegistrationForm` |
| URL name | `snake_case` | `user_detail`, `order_list` |
| Template | `snake_case.html` | `user_detail.html` |
| App | `lowercase` | `users`, `orders` |

## Project-Specific Conventions

### PEP 8 Overrides (in pyproject.toml)

- **Line length**: 88 (not PEP 8's 79) - black's default
- **Ignored rules**: `E501` (formatter handles), `DJ001` (we allow nullable CharField for legacy data)
- **Per-file ignores**: Tests allow `assert`, migrations ignore style rules

### Service Layer Pattern

- Business logic in `services.py`, not views
- Complex queries in `selectors.py`
- Services use keyword-only arguments: `def create_order(*, user, items):`

### Type Hints

All public functions require type hints. See `pyproject.toml` for mypy strictness settings.

---

## Change Log

| Date | Change | Rationale |
|------|--------|-----------|
| 2024-01-15 | Added DJ001 ignore | Legacy data has nullable CharFields |
| 2023-11-20 | Initial conventions | Project setup |
