# C Build & Run Commands

## Prerequisites

- GCC 9+ or Clang 10+
- Make 4.0+
- Optional: CMake, Valgrind, clang-format, cppcheck

```bash
# Ubuntu/Debian
sudo apt install build-essential cmake valgrind clang-format cppcheck

# macOS
xcode-select --install
brew install cmake clang-format cppcheck
```

## Quick Reference

```bash
make                    # Build (debug)
make release            # Build (optimized)
make test               # Run tests
make clean              # Remove artifacts
./build/debug/myproj    # Run
```

## Additional Commands

```bash
# Analysis
make check              # Static analysis (cppcheck)
make format             # Format code (clang-format)
valgrind ./build/debug/myproj  # Memory check

# Debugging
make debug              # Build with debug symbols
gdb ./build/debug/myproj
```

## Build System

Check `Makefile` (or `CMakeLists.txt`) for full target list and configuration.

---

## Change Log

| Date | Change | Rationale |
|------|--------|-----------|
| [Date] | Initial build setup | Project setup |
