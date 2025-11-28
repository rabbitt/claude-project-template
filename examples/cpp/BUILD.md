# C++ Build & Run Commands

## Prerequisites

- GCC 10+ or Clang 12+ (for C++17/20)
- CMake 3.16+
- Optional: Ninja, vcpkg/Conan, clang-format, clang-tidy

```bash
# Ubuntu/Debian
sudo apt install build-essential cmake ninja-build clang-format clang-tidy

# macOS
brew install cmake ninja llvm
```

## Quick Reference

```bash
# Configure & Build
cmake -B build -G Ninja
cmake --build build

# Test
ctest --test-dir build
# or
./build/tests/myproj_tests

# Clean
rm -rf build
```

## Additional Commands

```bash
# Build variants
cmake -B build -DCMAKE_BUILD_TYPE=Debug
cmake -B build -DCMAKE_BUILD_TYPE=Release

# Code quality
clang-format -i src/**/*.cpp include/**/*.h
clang-tidy src/*.cpp -- -std=c++20 -Iinclude

# With vcpkg
cmake -B build -DCMAKE_TOOLCHAIN_FILE=$VCPKG_ROOT/scripts/buildsystems/vcpkg.cmake
```

## Build System

Check `CMakeLists.txt` for full configuration, targets, and options.

---

## Change Log

| Date | Change | Rationale |
|------|--------|-----------|
| [Date] | Initial build setup | Project setup |
