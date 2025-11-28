# C Coding Conventions

## Style Guide

Choose a base style and configure tooling to enforce it:

| Style | Description | Reference |
|-------|-------------|-----------|
| Linux Kernel | Popular for systems code | [kernel.org/doc/html/latest/process/coding-style.html](https://www.kernel.org/doc/html/latest/process/coding-style.html) |
| GNU | Used by GNU projects | [gnu.org/prep/standards](https://www.gnu.org/prep/standards/standards.html) |
| Google | Modern, well-documented | [google.github.io/styleguide/cguide.html](https://google.github.io/styleguide/cguide.html) |

## Tool Configuration

| Tool | Purpose | Config Location |
|------|---------|-----------------|
| clang-format | Code formatting | `.clang-format` |
| clang-tidy | Static analysis | `.clang-tidy` |
| cppcheck | Additional checks | Command-line flags or config |

**Check the config files** - they ARE the conventions. The AI should read `.clang-format` to understand project formatting rules.

**Before committing:**
```bash
clang-format -i src/*.c src/*.h
clang-tidy src/*.c -- -Iinclude
```

## Common C Patterns

| Type | Pattern | Example |
|------|---------|---------|
| Variables | `snake_case` | `user_count`, `file_path` |
| Functions | `snake_case` | `calculate_total()`, `init_module()` |
| Constants/Macros | `UPPER_SNAKE_CASE` | `MAX_BUFFER_SIZE`, `API_VERSION` |
| Types (struct/enum) | `PascalCase` | `UserData`, `LogLevel` |
| Enum values | `PREFIX_UPPER_CASE` | `LOG_LEVEL_DEBUG` |

## Project-Specific Conventions

<!--
Document ONLY:
- Your chosen base style (Linux, GNU, Google, etc.)
- Deviations from that style
- Module prefix conventions for your project
- Memory management patterns (who owns what)
- Error handling conventions

If it's enforced by clang-format/clang-tidy, don't repeat it here.
-->

[Add your project-specific conventions here]

---

## Change Log

| Date | Change | Rationale |
|------|--------|-----------|
| [Date] | Initial conventions | Project setup |
