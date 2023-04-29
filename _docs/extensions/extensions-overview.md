---
title: Overview
permalink: /docs/extensions-overview/
---

Minitest can be extended to support custom data types. Minitest uses C11's _Generic handle to identify the type for expect statements. You can add your own types by defining `MT_EXPECT_EXTENSIONS` before loading the Minitest header.

---

### Scope

The comparison operations when defining expect extensions have access to the following variables:

- MiniTest *mt
  - Minitest pointer

- (type / array) actual
  - Comparator value

- size_t actual_size
  - Size of the comparator

- int negated
  - Invert the function result

- (type / array) expected
  - Value of the expect() comparator

- size_t expected_size
  - Size of the expect() comparator

- (type) max_range
  - Max range value for in_range assertions

- size_t max_range_size
  - Max range size for in_range assertions

- mt_expect_flags flag
  - Assertion flag type (eg MT_EQUALS)

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

---

### Notes

You must define a `__format_<function_identifier>(data_type value)` handler that returns the appropriate value associated with `printf_format` with expect extensions.

If you do not want to print out any custom error messages, you can define your extension with `mt_expect_ext_default` or `mt_expect_array_ext_default` to define and use a default handler:

```c
void* __format_<function_identifier>(data_type value) { return NULL; }
```

---

### Available Macros

#### mt_expect_forward(function_identifier, data_type)

Creates the forward definition of the expect function.

```c
mt_expect_forward(extstruct, ExpectExt*);
```

---

#### mt_expect_array_forward(function_identifier, data_type)

Creates the forward definition of the expect function for an array.

```c
mt_expect_array_forward(intarr, int);
```

---

#### mt_setup_expect_forwards( VA_ARGS )

A list separated by a space or newline containing `mt_expect_forward` and `mt_expect_array_forward` definitions,

```c
mt_setup_expect_forwards(
  mt_expect_forward(extstruct, ExpectExt*)
  mt_expect_array_forward(extstructarr, ExpectExt*)
)
```

---

#### mt_expect_ext(function_identifier, data_type, comparison, printf_format)

Defines the expect function. Two variables are exposed in this context:

- data_type actual
- data_type expected

comparison can be any C expression or function call passing in the actual and expected variables.

printf_format is any printf format to display if the expectation fails. You can pass NULL if you do not want to print any error message.

---

#### mt_expect_array_ext(function_identifier, data_type, comparison, printf_format)

Defines the expect function for arrays. Two variables are exposed in this context:

- data_type actual
- data_type expected

comparison can be any C expression or function call passing in the actual and expected variables.

printf_format is any printf format to display if the expectation fails. You can pass NULL if you do not want to print any error message.

---

#### mt_setup_expect_extensions( VA_ARGS )

A list of `mt_expect_extension` definitions separated by a space or newline. Use `mt_setup_expect_extensions` to generate the `MT_EXPECT_EXTENSIONS` definition.
