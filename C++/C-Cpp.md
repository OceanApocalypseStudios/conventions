# C/C++ Conventions
<img src="https://raw.githubusercontent.com/vscode-icons/vscode-icons/refs/heads/master/icons/file_type_cpp.svg" alt="C++" align=right width="80" />

List of C/C++ conventions used at OceanApocalypseStudios.

> Made by Norb.

----

## Naming

Element | Naming Convention | Example
------- | ----------------- | -------
Classes and Structs | [PascalCase](https://wiki.c2.com/?PascalCase) | `class MyClass {...};`, `struct MyStruct {...};`
Methods and functions | [snake_case](https://stringcase.org/cases/snake/) | `void my_func() {...}`, `void MyClass::my_method() {...}`
Custom types (using typedef) | [snake_case](https://stringcase.org/cases/snake/) | `typedef uint unsigned int;`, `typedef void (*my_func_t)(void);`
Macros | [CONSTANT_CASE](https://stringcase.org/cases/constant/) | `#define MY_NUM 0`, `#define MIN(a,b) (a<b)?a:b`
Variables, parameters and template parameters | [PascalCase](https://wiki.c2.com/?PascalCase) | `int MyNum = 0;`, `int* MyNumPtr = &MyNum;`, `void my_func(int MyNumber, int* PtrToMyOtherNumber)`, `template<typename Type, class MyClass> ...`

----

## Other styles

Use tabs for indentation!!!

Do not use default types like `int`, `short`, `long long` etc. as these change depending on platforms (For example `int` is 4 bytes on 32bit platforms but is not guaranteed to be that same size on say, 16bit platforms.)
Instead, use the `stdint.h` (`cstdint` if using C++) that defines useful macros to guarantee data type sizes. (`uint32_t` for example is ALWAYS 32 bits).

As much as we like `#pragma once`, it is better to do header guards the classical way:

```c
#ifndef MY_LIBRARY
#define MY_LIBRARY
// Header here
#endif
```

Because `#pragma once` is apparently "supported by many compilers but is not standard" and thus may not work with
super obscure compilers. But if you're not using GCC or MSVC we can't help you anyway.

The pointer asterisk is always on the left. Example: `int* MyNumPtr = &MyNum;`. Period. I know I know, someone will come up bringing up something like `int* A,B;` but anyone skilled in C/C++ syntax will know that A is an int pointer and B is just int, and because of that defining multiple variables is something I (norbcodes) personally avoid.

```cpp
int* A,B;
// Is the same as
int* A;
int B;
```

Project structure is defined as the following:

```c
{ProjectName}
|- src/  // All .c, .cpp etc. files go here
|- src/data/  // ANY type of data that is to be directly embedded into the executable
|- include/{ProjectName}/  // All our headers go here
|- include/{...}/  // Headers that are not ours
|- lib/  // .a files go here
|- lib/shared/  // .dll / .so go here. These should be copied along with the exe using whatever method available
|- cmake/{ProjectName}/  // Any cmake modules only for our project
|- cmake/  // Other cmake modules
```

## TODO

- [ ] Add more coding conventions
