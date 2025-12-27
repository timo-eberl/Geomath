# Geomath

A lightweight, header-based C++20 vector math library designed for geometric calculations.

## Features

- **Generic Vectors:** Templated `Vector<n, T>` implementation.
- **Type Aliases:** Pre-defined types for common needs (e.g., `Vector3`, `IntVector2`).
- **Specializations:** `Vector2`, `Vector3`, `Vector4` have named component access (`.x`, `.y`, `.z`, `.w`) and swizzling-style subsets (`.xy`, `.xyz`).
- **Vector Math:** All common operations including `dot`, `cross`, `lerp`, `normalize`, `distance`, `clamp`, and component-wise arithmetic.
- **Comparison:** Approximate equality checks (`equals_approx`) for floating-point stability.

## Requirements

- C++ 20 or higher
- CMake 3.10+ (for build integration)

## Integration

Since the project is built with CMake, you can simply include the directory and link the library:

```cmake
add_subdirectory(geomath)
target_link_libraries(your_project PRIVATE geomath)
```

## Usage Example

```cpp
#include <geomath.h>
#include <iostream>

int main() {
	// Flexible initialization (mixed numeric types allowed)
	gm::Vector3 a(1, 2, 3);
	gm::Vector3 b({ -0.3f, 1, 5u });

	// Composition: Construct larger vectors from smaller ones
	gm::Vector4 pos(a, 1.0); 

	// Scalar broadcasting
	gm::Vector3 offset = a + 0.5; // Adds 0.5 to all components: { 1.5, 2.5, 3.5 }

	// Geometric helper functions
	gm::Vector3 mid = gm::lerp(a, b, 0.5);
	double dist = gm::distance(a, b);

	// Component access (Swizzling)
	gm::Vector2 xy = pos.xy;

	// Floating-point stable comparison
	if (gm::equals_approx(a, b)) {
		std::cout << "Vectors are approximately equal.\n";
	}

	// Result: { 0.35, 1.5, 4 }
	std::cout << "Result: " << mid << std::endl;

	return 0;
}
```

## Testing

The project includes unit tests using CTest.

```bash
mkdir build && cd build
cmake ..
make
ctest
```
