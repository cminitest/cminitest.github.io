---
title: Build Configuration
permalink: /docs/build-configuration/
---

Certain functionality of Minitest can only be modified through preprocessor macros defined at compile time and Makefile variables. The Minitest build system makes assumptions on the default C compiler for each system and environment.

### LD_WRAP

The definition of LD_WRAP tells minitest that the linker, or object files, will have their function definitions wrapped (see ld3's <a href="https://ftp.gnu.org/old-gnu/Manuals/ld-2.9.1/html_node/ld_3.html" target="_blank">--wrap</a> argument ).

If a function `add` is wrapped, it will be renamed `__real_add`. Any calls to `add` will be replaced with `__wrapped_add`. This is the expected behavior for Minitest's mocking capabilities.

**NOTE:** If your linker does not support --wrap or you do not modify your object files to follow the wrap convention, mocking capabilities may trigger a segmentation fault if this flag is defined.

<hr />

Defined in: <a href="https://github.com/cminitest/minitest/blob/master/Makefile.in#L29" target="_blank">Makefile.in</a> line 29.

Defined in: <a href="https://github.com/cminitest/minitest/blob/master/Makefile.in#L35" target="_blank">Makefile.in</a> line 35.

### TESTWRAPDMP

TESTWRAPDMP is a flag used to specify the mocking capabilities for the test suite. This triggers binutils gobjcopy to simulate --wrap by redefining function(s) to be mocked and tested.

If you do not have binutils installed, set this flag to 0 in the Makefile.in.

<hr />

Defined in: <a href="https://github.com/cminitest/minitest/blob/master/Makefile.in#L36" target="_blank">Makefile.in</a> line 36.

### AC_PROG_CC([gcc])

By default, the autoconfigure (autoconf) script looks for the gcc compiler. This is often an alias to the system C compiler if GNU gcc is not installed. If you want to use a specific C compiler, update this value.

Defined in: <a href="https://github.com/cminitest/minitest/blob/master/configure.ac#L3" target="_blank">configure.ac</a> line 3.