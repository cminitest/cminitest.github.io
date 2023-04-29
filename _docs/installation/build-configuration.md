---
title: Build Configuration
permalink: /docs/build-configuration/
---

Certain functionality of Minitest can only be modified through preprocessor macros defined at compile time and Makefile variables. The Minitest build system makes assumptions on the default C compiler for each system and environment.

### AC_PROG_CC([gcc])

By default, the autoconfigure (autoconf) script looks for the gcc compiler. This is often an alias to the system C compiler if GNU gcc is not installed. If you want to use a specific C compiler, update this value.

Defined in: <a href="https://github.com/cminitest/minitest/blob/master/configure.ac#L3" target="_blank">configure.ac</a> line 3.