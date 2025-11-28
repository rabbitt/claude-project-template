# Python Library Structure

## Standard Layout

We follow [PyPA's src layout](https://packaging.python.org/en/latest/discussions/src-layout-vs-flat-layout/).

```
mypackage/
├── src/mypackage/          # Source code
│   ├── __init__.py         # Public API
│   ├── py.typed            # PEP 561 type marker
│   └── ...
├── tests/                  # Tests (pytest)
├── docs/                   # Documentation
├── pyproject.toml          # Project config
└── README.md
```

## Where Code Goes

| Type | Location |
|------|----------|
| Public API | `src/mypackage/__init__.py` |
| Internal code | `src/mypackage/_internal/` |
| Tests | `tests/test_*.py` |
| Fixtures | `tests/conftest.py` |

## Project-Specific Notes

<!--
Document ONLY deviations from standard src layout
-->

[Add your project-specific structure notes here]

---

## Change Log

| Date | Change | Rationale |
|------|--------|-----------|
| [Date] | Initial structure | Project setup |
