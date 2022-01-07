---
title: Overview
permalink: /docs/assertions-overview/
---

Minitest provides many default assertions for core C data types to get you started. You can also write your own <a href="/docs/extensions-overview/">extensions</a> for custom data types.

### Core Assertion Types

- int, int[] (int*)
- char, char*
- short, short[] (short*)
- long, long[] (long*)
- double, double[] (double*)
- float, float[] (float*)
- void*
- size_t
- unsigned char
- unsigned short
- unsigned int
- unsigned long

### Syntax

All assertions in minitest begin with the `expect(actual)` macro. Expect determines the appropriate assertion function to use for the data type of `actual` -- including any extensions you create.

Immediately after `expect()` you must define `to` in order to generate the proper assertion function call.

```
expect(actual) to [not | be | have] [assertion_type | assertion_type(expected)]
```

Depending on your assertion, you can invert the assertion with the optional `not` macro. `be` and `have` are also optional and offer no specific functionality other than assertion syntactic sugar.

Some assertion types for the expected result accept parameters, others do not. Those that do not are prefixed with `be_` and assert a specific data type. For example:

```
expect(actual) to be_null
```

All other assertions take in the `expected` argument. 