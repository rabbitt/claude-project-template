# Python Coding Conventions

## Style Guide

We follow [PEP 8](https://peps.python.org/pep-0008/) and [PEP 257](https://peps.python.org/pep-0257/) (docstrings), enforced by tooling.

## Tool Configuration

| Tool | Purpose | Config Location |
|------|---------|-----------------|
| ruff | Linting + formatting | `pyproject.toml` [tool.ruff] |
| mypy | Type checking | `pyproject.toml` [tool.mypy] |
| pytest | Testing | `pyproject.toml` [tool.pytest] |

**Check the config files** - they ARE the conventions. The AI should read these to understand project-specific rules.

**Before committing:**
```bash
ruff check . && ruff format --check . && mypy .
```

## Project-Specific Conventions

<!--
Document ONLY:
- Deviations from PEP 8
- Project-specific patterns not covered by tooling
- Architectural decisions about code organization

If it's enforced by ruff/mypy, don't repeat it here.
-->

[Add your project-specific conventions here]

---

## Change Log

| Date | Change | Rationale |
|------|--------|-----------|
| [Date] | Initial conventions | Project setup |
