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

### Example

**Library.c**

```c
{% include examples/assertions/beencalled/lib.c %}
```

**main.c**

```c
{% include examples/assertions/beencalled/main.c %}
```