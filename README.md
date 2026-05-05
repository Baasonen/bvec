# bvec

A simple vector and matrix library for C, intended for my personal projects and 2D/3D graphics. It provides essential linear algebra functionality with a focus on simplicity and ease of integration.

## Features

* **Header-only**: Easy to include in any project without complex build systems.
* **C / C++ Compatible**: Supports C11 and above.
* **Static inline functions**
* **Zero Dependencies**: Uses `math.h` by default, but can be used without it by providing custom macros.
* **Type Safety**: Uses unions for vector types, allowing access via named components (e.g. `.x`, `.y`, `.z`, `.w`) or indexed elements (e.g. `.elements[i]`).
* **Row-Major**: Matrices are stored in row-major order.

## Data Types

| Type | Description |
| :--- | :--- |
| `vec2`, `vec3`, `vec4` | Float-based vectors of size 2, 3, and 4. |
| `mat2`, `mat3`, `mat4` | Float-based square matrices of size 2x2, 3x3, and 4x4. |

### Conventions
* Row-major matrices
* Right-handed coordinate system
* OpenGL style clip space projection

## Vector Operations

### Initialization
* `vecNMake`: Create a vector with specific values.
* `vecNZero`: Create a vector with all components set to zero.

### Arithmetic
* `vecNAdd`: Component-wise addition.
* `vecNSub`: Component-wise subtraction.
* `vecNScale`: Multiply a vector by a scalar.

### Mathematical Functions
* `vecNDot`: Dot product of two vectors.
* `vecNCross`: Cross product (available for `vec2` and `vec3`, **NOTE:** 2D returns a scalar).
* `vecNLength`: Calculate the magnitude of a vector.
* `vecNLengthSq`: Calculate the squared magnitude (useful for performance).
* `vecNNormalize`: Return a unit vector in the same direction (Returns 0 for zero length vectors).

### Linear Algebra
* `vecNAngle`: Find the angle between two vectors.
* `vec3Lerp`: Linear interpolation between two vectors (`vec3` only).
* `vec3Reflect`: Reflect a vector across a surface normal (`vec3` only).
* `vec3Project`: Project one vector onto another (`vec3` only).

## Matrix Operations

### Initialization
* `matNIdentity`: Create an identity matrix.
* `matNZero`: Create a matrix with all elements set to zero.
* `matNDiag`: Create a diagonal matrix from a set of values.

### Transformation & Basic Operations
* `matNTranspose`: Flip a matrix over its diagonal.
* `matNScale`: Scale a matrix by a scalar.
* `mat4Mul`: Multiply two `mat4` matrices.
* `mat4Mul4Vec4`: Multiply a `mat4` by a `vec4`.

### 3D Utilities (`mat4`)
* `mat4Translate(vec3)`: Create a translation matrix.
* `mat4Rotate(axis, angle)`: Create a rotation matrix around a specific axis.
* `mat4ScaleVec3(vec3)`: Create a scaling matrix from a `vec3`.
* `mat4Transform(trans, axis, angle, scale)`: Combine translation, rotation, and scaling into one matrix.
* `mat4LookAt(eye, target, up)`: Generate a view matrix.
* `mat4Perspective(fov, aspect, near, far)`: Generate a perspective projection matrix.

### Usage Example
```
#include "bvec.h"

void setup_camera()
{
    vec3 eye = vec3Make(0.0f, 5.0f, 10.0f);
    vec3 target = vec3Zero();
    vec3 up = vec3Make(0.0f, 1.0f, 0.0f);

    // Create View Matrix
    mat4 view = mat4LookAt(eye, target, up);

    // Create Projection Matrix
    mat4 projection = mat4Perspective(45.0f, 16.0f / 9.0f, 0.1f, 100.0f);
    
    // Combine them
    mat4 viewProj = mat4Mul(projection, view);
}
```

## Configuration
If the standard library is not available, define BVEC_NO_STD_LIB before providing your own math implementation
```
#define BVEC_NO_STD_LIB
#define BVEC_SQRT(x) my_custom_sqrtf(x)
#include "bvec.h"
```

## License
This project is licensed under the GPLv2 Licence - See LICENSE file for details

Copyright (c) 2026 Henri Paasonen 
