---
title: Expect
permalink: /docs/extensions-expect/
---

To extend the expect() assertion to support custom data types, your test suite headers must define `MT_EXPECT_EXT` before loading `minitest.h`.

### Macros

Minitest defines the following macros to add data types to the expect assertion chain.

#### mt_register_expect_extension(function_identifier, data_type)

Adds a `_Generic` handle for the passed in `data_type` to the expect() handler, pointing to the function 

```c
void __expect_<function_identifier>(
  MiniTest *mt,
  type actual arr,
  size_t actual_size,
  int negated,
  type expected arr,
  size_t expected_size,
  type max_range arr,
  size_t max_range_size,
  mt_expect_flags flag
);
```

### Example

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