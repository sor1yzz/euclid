# Eucild - a Graphics Mathematics Library

**Features**
- Compile-time calculation (part in clang)
- C++20 Module support (WIP)

## Introduction
- Euclid uses **row-major** order
- Euclid requires AVX2 support

- Compile-time Calculation
  ```c++
  using namespace euclid;
  constexpr Vec4 a { 1,2,3,0 };
  constexpr Vec4 b { 4,5,6,0 };
  constexpr Vec4 res1 = a + b;
  constexpr Vec4 res2 = dot(a, b);
  constexpr Vec4 res3 = cross(a, b);
  ```
  
- Print Euclid Components
  ```c++
  #include <Euclid/Euclid.h>
  #include <Euclid/Print.hpp>

  using namespace euclid;

  Vec4 v{ 1,2,3,4 };
  Mat2 m{ 1,2,
          3,4 };
  debug::print(v, m);
  ```

- `Transformation` (WIP)

## Tested Compiler
- MSVC 19.29
- GCC 11.3
- Clang 13.0