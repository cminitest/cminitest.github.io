---
title: MacOS
permalink: /docs/install-macos/
---

MacOS, by default, provides an alias for gcc. This alias points to clang and Apple's LLVM.


### 1. Generate the configure script

autoconf will generate the configure bash script to find required dependencies.

```bash
autoconf
```

### 2. Generate the makefile

configure will create the final makefile, filling in variables and C flags with what's defined in configure.ac

```bash
./configure
```

### 3. Build the shared library

make sharedlib will compile the minitest library to `lib/libminitest.so`.

```bash
make sharedlib
```

### 4. Install the library

Install the shared library to `/usr/local/lib` and the headers to `/usr/local/include/minitest`.

```bash
make install
```

### 5. Build and run the test suite


```bash
make tests ; ./bin/testsuite
```

### 6. Alternative

The default make command will run all of the above commands. Use only after reviewing the generated Makefile.

```bash
make
```