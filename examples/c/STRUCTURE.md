# C Project Structure

## Standard Layout

```
myproj/
├── include/myproj/         # Public headers
├── src/                    # Source files + private headers
│   └── internal/           # Private headers
├── tests/                  # Test files
├── build/                  # Build output (gitignored)
├── Makefile                # or CMakeLists.txt
└── .clang-format
```

## Where Code Goes

| Type | Location |
|------|----------|
| Public headers | `include/myproj/*.h` |
| Private headers | `src/internal/*.h` |
| Implementation | `src/*.c` |
| Tests | `tests/test_*.c` |

## Project-Specific Notes

<!--
Document ONLY:
- Deviations from standard layout
- Third-party dependencies
- Platform-specific directories
-->

[Add your project-specific structure notes here]

---

## Change Log

| Date | Change | Rationale |
|------|--------|-----------|
| [Date] | Initial structure | Project setup |
