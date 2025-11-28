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

<!--
Document ONLY:
- Deviations from PEP 8 or Django conventions
- Project-specific patterns (service layer, selectors, etc.)
- Architectural decisions about code organization

If it's enforced by ruff/mypy or is standard Django, don't repeat it here.
-->

[Add your project-specific conventions here]

---

## Change Log

| Date | Change | Rationale |
|------|--------|-----------|
| [Date] | Initial conventions | Project setup |
