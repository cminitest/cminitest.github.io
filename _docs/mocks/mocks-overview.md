---
title: Overview
permalink: /docs/mocks-overview/
---

Minitest supports mocking through alias symbols, symbol replacement, or compilation macros. For example, with GCC you can specify the `--wrap=` parameter for a function.

```
gcc -Wl,--wrap=add_ints -o main main.c
```

### For linkers that do not support --wrap

GNU binutils provide binary utilities to manipulate objects and libraries. To use mocking with a linker, you must redefine the symbols in your object files to follow the conventions of linkers that support --wrap.

NOTE: this option is limited as symbols in the object file where `__real` is defined will always reference `__real`, whereas `--wrap` replaces function definitions with `__real_<function name>` and function references with `__wrap_<function name>`.

**Replace all references with __wrap**

```
gobjcopy  --redefine-sym _add_ints=___wrap_add_ints mylib.o obj1.o obj2.o
```

**Redefine the real function in the library**

```
$> gobjcopy mylib.o --redefine-sym ___wrap_add_ints=___real_add_ints mylib.o
```

### Macros

Minitest defines the following macros to manage mocking.

#### mt_mock_forwards(function_ptr, return_type, arg_1_type, arg_2_type ...)

**Note:** Make forward calls only in your header file(s).

mt_mock_forwards makes the forward definition for the `__wrapper_<function_name>` function. It also defines the appropriate data structure to support mocking and tracking calls.

```c
mt_mock_forwards(add_two_ints, int, int n1, int n2);
```

#### mt_mock_args(arg_name_1, arg_name_2 ...)

Creates a list of arguments to pass from the `__wrapper` function to `__real` when released.

```c
mt_mock_args(n1,n2)
```

#### mt_define_mock(function_ptr, arg_names, return_type, type arg_name, type arg_name ...);

Defines the `__wrap_<function_name>(type arg_name...)` function handler.

```c
mt_define_mock(add_two_ints, mt_mock_args(n1,n2), int, int n1, int n2);
```
