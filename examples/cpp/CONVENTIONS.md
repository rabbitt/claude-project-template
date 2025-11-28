# C++ Coding Conventions

## Style Guide

Choose a base style and configure tooling to enforce it:

| Style | Description | Reference |
|-------|-------------|-----------|
| Google | Comprehensive, modern | [google.github.io/styleguide/cppguide.html](https://google.github.io/styleguide/cppguide.html) |
| LLVM | Used by Clang/LLVM | [llvm.org/docs/CodingStandards.html](https://llvm.org/docs/CodingStandards.html) |
| Mozilla | Firefox codebase | [firefox-source-docs.mozilla.org](https://firefox-source-docs.mozilla.org/code-quality/coding-style/index.html) |
| C++ Core Guidelines | Advisory, not style | [isocpp.github.io/CppCoreGuidelines](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines) |

## Tool Configuration

| Tool | Purpose | Config Location |
|------|---------|-----------------|
| clang-format | Code formatting | `.clang-format` |
| clang-tidy | Static analysis + modernization | `.clang-tidy` |
| cppcheck | Additional static analysis | Command-line or config |

**Check the config files** - they ARE the conventions. The AI should read `.clang-format` and `.clang-tidy` to understand project rules.

**Before committing:**
```bash
clang-format -i src/**/*.cpp include/**/*.h
clang-tidy src/**/*.cpp -- -std=c++20 -Iinclude
```

## Common C++ Patterns

| Type | Pattern | Example |
|------|---------|---------|
| Namespaces | `snake_case` | `my_project::utils` |
| Classes/Structs | `PascalCase` | `UserManager`, `Config` |
| Functions | `snake_case` or `camelCase` | `process_request()` |
| Variables | `snake_case` | `user_count` |
| Constants | `kPascalCase` or `UPPER_CASE` | `kMaxSize`, `MAX_SIZE` |
| Private members | trailing `_` | `name_`, `count_` |

## Project-Specific Conventions

<!--
Document ONLY:
- Your chosen base style (Google, LLVM, etc.)
- C++ standard version (C++17, C++20, etc.)
- Deviations from the base style
- Smart pointer conventions (unique_ptr vs shared_ptr usage)
- Error handling (exceptions vs error codes)

If it's enforced by clang-format/clang-tidy, don't repeat it here.
-->

[Add your project-specific conventions here]

---

## Change Log

| Date | Change | Rationale |
|------|--------|-----------|
| [Date] | Initial conventions | Project setup |
