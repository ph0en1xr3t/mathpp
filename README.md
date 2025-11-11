# mathpp

A modern C++20 mathematics library demonstrating modern CMake practices and C++20 features.

## Features

- **C++20 Concepts**: Type-safe generic programming with concepts
- **Modern CMake**: Clean, maintainable build configuration (CMake 3.20+)
- **Header-only templates**: Easy integration
- **Three-way comparison operator**: Spaceship operator (`<=>`)
- **std::format**: Modern string formatting (requires compiler support)

## Requirements

- CMake 3.20 or higher
- C++20 compatible compiler:
  - GCC 10+ 
  - Clang 13+
  - MSVC 19.29+ (Visual Studio 2019 16.11+)
  - Apple Clang 13+ (Xcode 13+)

## Building

### Quick Start

```bash
# Create build directory
mkdir build && cd build

# Configure
cmake ..

# Build
cmake --build .

# Run example
./mathpp_example
```

### With specific generator

```bash
# Unix Makefiles
cmake -G "Unix Makefiles" -B build
cmake --build build

# Ninja (faster builds)
cmake -G Ninja -B build
cmake --build build

# Xcode
cmake -G Xcode -B build
open build/mathpp.xcodeproj
```

### Build types

```bash
# Debug build (default)
cmake -DCMAKE_BUILD_TYPE=Debug -B build

# Release build (optimized)
cmake -DCMAKE_BUILD_TYPE=Release -B build

# With specific compiler
cmake -DCMAKE_CXX_COMPILER=clang++ -B build
```

## Project Structure

```
mathpp/
├── CMakeLists.txt          # Main CMake configuration
├── README.md               # This file
├── .gitignore             # Git ignore patterns
├── include/               # Public headers
│   └── mathpp/
│       └── vector.hpp     # Vector class with C++20 features
├── src/                   # Source files
│   └── vector.cpp         # Implementation
└── examples/              # Example applications
    └── main.cpp           # Example usage
```

## Usage Example

```cpp
#include <iostream>
#include <format>
#include "mathpp/vector.hpp"

int main() {
    using namespace mathpp;
    
    Vector<double> v1{1.0, 2.0, 3.0};
    Vector<double> v2{4.0, 5.0, 6.0};
    
    auto v3 = v1 + v2;
    double dot = v1.dot(v2);
    double mag = v1.magnitude();
    
    std::cout << std::format("v1 + v2 = [{}, {}, {}]\n", 
                             v3[0], v3[1], v3[2]);
    std::cout << std::format("v1 · v2 = {}\n", dot);
    std::cout << std::format("|v1| = {:.3f}\n", mag);
    
    return 0;
}
```

## C++20 Features Demonstrated

- **Concepts**: `Numeric` concept for type constraints
- **Three-way comparison**: `operator<=>` with default implementation
- **Ranges**: Range-based for loops with custom iterators
- **std::format**: Modern string formatting
- **Template improvements**: Cleaner syntax and better error messages

## Troubleshooting

### std::format not available

If your compiler doesn't support `std::format` yet, replace it with:
```cpp
#include <iostream>
std::cout << "v1 · v2 = " << dot << "\n";
```

Or use the fmt library as a fallback:
```bash
# Install fmt
# Add to CMakeLists.txt:
find_package(fmt REQUIRED)
target_link_libraries(mathpp PRIVATE fmt::fmt)
```

### Compiler errors with concepts

Ensure you're using a fully C++20 compliant compiler. Check your compiler version:
```bash
g++ --version      # GCC
clang++ --version  # Clang
```

## License

MIT License - feel free to use this as a template for your own projects.
