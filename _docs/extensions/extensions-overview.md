---
title: Overview
permalink: /docs/extensions-overview/
---

Minitest can be extended to support custom data types. Minitest uses C11's _Generic handle to identify the type for expect statements. You can add your own types by defining `MT_EXPECT_EXT` before loading the Minitest header.

### Macros

#### mt_expect_forward(function_identifier, data_type)

Creates the forward definition of the expect function.

```c
mt_expect_forward(extstruct, ExpectExt*);
```

#### mt_expect_array_forward(function_identifier, data_type)

Creates the forward definition of the expect function for an array.

```c
mt_expect_array_forward(intarr, int);
```

#### mt_expect_ext(function_identifier, data_type, comparison, printf_format)

Defines the expect function. Two variables are exposed in this context:

- data_type actual
- data_type expected

comparison can be any C expression or function call passing in the actual and expected variables.

printf_format is any printf format to display if the expectation fails. You can pass NULL if you do not want to print any error message.

**NOTE:**

You must define a `__format_<function_identifier>(data_type value)` handler that returns the appropriate value associated with `printf_format`.

If you do not want to print out any custom error messages, you can define your extension with `mt_expect_ext_default` or `mt_expect_array_ext_default` to define and use a default handler:

```c
void* __format_<function_identifier>(data_type value) { return NULL; }
```
