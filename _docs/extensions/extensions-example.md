---
title: Example
permalink: /docs/extensions-example/
---

Assertion extensions are broken up into forwards, expectation setup, assertion definition, and output format.

---

#### Forwards

Forwards are defined in the header for defining `MT_EXPECT_EXTENSIONS`. The `MT_EXPECT_EXTENSIONS` macro is inserted into the `_Generic` expectation call function if defined. 

```c
mt_setup_expect_forwards(
  mt_expect_forward(extstruct, ExpectExt*)
  mt_expect_array_forward(extstructarr, ExpectExt*)
)
```

---

#### Expectation Setup

After defining forwards, the `MT_EXPECT_EXTENSIONS` macro in your header file is to be defined with `mt_setup_expect_extensions`, space or newline delimited list containing `mt_expect_extension` definitions matching the forwards.

```c
#define MT_EXPECT_EXTENSIONS mt_setup_expect_extensions( \
  mt_expect_extension(extstruct, ExpectExt*)             \
  mt_expect_extension(extstructarr, ExpectExt**)         \
)
```

---

#### Assertion Definition

Assertion definitions are created by the `mt_expect_ext`, `mt_expect_array_ext`, `mt_expect_ext_default`, and `mt_expect_array_ext_default` macros. Any post-fixed macros with `default` must take `NULL` as the printf format to create a generic error message handler. Assertions can be a function call or C expression.

```c
#include "testsuite.h"

int __assert_array_extstructarr(ExpectExt* arr_1[], ExpectExt* arr_2[], size_t s1, size_t s2) {
  if (s1/sizeof(ExpectExt*) != s2/sizeof(ExpectExt*)) { return 0; }
  return 1;
}

mt_expect_ext(extstruct, ExpectExt*, (actual->value == expected->value), "%i");
mt_expect_array_ext_default(extstructarr, ExpectExt*, __assert_array_extstructarr(expected, actual, actual_size, expected_size), NULL);
```

---

#### Output Format

Output formats, excluding those post fixed with `default` are to return a value associated with the printf expression.

```c
// defined in the header:
//    mt_expect_ext(extstruct, ExpectExt*, (actual->value == expected->value), "%i");
//

// format function matching %i
int __format_extstruct(ExpectExt* extstruct) {
  return extstruct->value;
}
```

---

### Full Example

**testsuite.h**

```c
{% include examples/extensions/custom_format/testsuite.h %}
```

**extension.c**

```c
{% include examples/extensions/custom_format/extension.c %}
```

**main.c**

```c
{% include examples/extensions/custom_format/main.c %}
```