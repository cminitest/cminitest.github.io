---
title: MacOS
permalink: /docs/install-macos/
---

MacOS, by default, provides an alias for gcc. This alias points to clang and Apple's LLVM. The Apple LLVM, linker, and clang implementation does not support mocking. The minitest library and headers will compile and install as expected, but the test suite will return a non-0 status code (or segmentation fault).

### Optional: Install GNU Binutils and Homebrew

If using the Apple LLVM, GNU Binutils offer functionality to simulate the behaviors of `--wrap`. <a href="https://brew.sh/" target="_blank">Homebrew<a/> offers an automated solution to installing binutils.

```sh
brew install binutils
```

### If not using GNU Binutils

If you choose to not install GNU Binutils, the minitest test suite will return a non-0 status code or segmentation fault. You must remove the `LD_WRAP` flag from the test suite compilation and `TESTWRAPDMP` must be set to 0. This can be found in <a href="https://github.com/cminitest/minitest/blob/master/Makefile.in#L35-L36" target="_blank">Makefile.in</a>.

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
sudo make
```