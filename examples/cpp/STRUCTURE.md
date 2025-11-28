# C++ Project Structure

## Standard Layout

```
myproj/
├── include/myproj/         # Public headers
├── src/                    # Source files + private headers
│   └── internal/           # Private headers
├── tests/                  # Test files
├── build/                  # Build output (gitignored)
├── CMakeLists.txt
├── .clang-format
└── .clang-tidy
```

## Where Code Goes

| Type | Location |
|------|----------|
| Public headers | `include/myproj/*.h` |
| Private headers | `src/internal/*.h` |
| Implementation | `src/*.cpp` |
| Tests | `tests/*_test.cpp` |
| Mocks | `tests/mocks/` |

## Project-Specific Notes

<!--
Document ONLY:
- Deviations from standard layout
- Third-party dependencies (vcpkg, Conan, vendored)
- Platform-specific directories
-->

[Add your project-specific structure notes here]

---

## Change Log

| Date | Change | Rationale |
|------|--------|-----------|
| [Date] | Initial structure | Project setup |
