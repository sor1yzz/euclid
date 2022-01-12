# Eucild - a Graphics Mathematics Library
> w11knd's Graphics Mathematics Library

## Overview
- **Euclid** 是一个基于 C++20 的图形数学库

**Features**

- 编译期的计算支持
- 编译期的类型约束
- `SIMD` Speed up (Requires AVX2 supported)
- Head-only

## Introduction
- 编译期的计算支持
  
  Better with C++23 `(if consteval)`

  暂时使用 `__builtin_is_constant_evaluated()` 来判断是否是常量求值上下文

  在使用 `constexpr` 创建变量时，IDE (Visual Studio) 可能会报错，但可以通过编译

- 编译期的类型约束
  
   使用 `concept`来约束某些操作
    
    **Euclid** 支持的算术类型类型有 `int, float`
  ```c++
  Vecotr<int, 3>; // OK
  Point<float, 3>; // OK
  Vector<char, 3>; // compile-time error
  ```
- `euclid::io::print(...args)`
  ```c++
  // 如要将数据打印到 Console，请在 <Euclid.h> 之后 
  // #include <Euclid_print.h>

  #include <Euclid.h>
  #include <Euclid_io.h>

  vec3i v1{ 1,2,0 };

  point3f p1 { 1.2f, 2.3f, 1.f };

  mat2i m1{ 1,  0,
            0, -1 };

  io::print(v1, p1, m1);

  ```

- `constexpr` 数学函数
  ```c++
  float res1 = math::cos(45);
  float res2 = math::sin(35.f)
  float res4 = math::sqrt(2);
  ```

- 类型转换

  ```c++
  vec4i v1{ 1,2,3,4 };
  vec4f = v1.castTofloat(); // 只支持 int cast to float
  ```

- `operator+=, *=, -=` 的约束
  ```c++
  vec2i v1{ 1, 2 };
  vec2f v2{ 1.1f, 2.2f };
  v1 *= 2.2f; // concept constraint is false: int *= float unacceptable precision loss
  v1 += v2; // same reason
  ```

- `Transformation in Homogeneous Coordinates`
  ```c++
  auto res = transform4d::scale(1, 2, 3); // res : mat4i 这里没有必要提升类型
  vec4i axis{ 0,0,1,0 };
  auto res1 = transform4d::rotate(axis, 45); // res1 : float
  auto res2 = transform4d::translate(1, 2, 3); // res2 : mat4i same reason with res
  auto res3 = transform4d::perspective(fov, aspectRatio, zNear, zFar); // 返回类型依据 Euclid 类型提升原则
  ```
## Tested Compiler
- Add compile flag /arch:AVX2, -mavx2
- MSVC 16.10/17.0
- GCC 11.2
