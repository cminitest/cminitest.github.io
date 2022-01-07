---
title: Describe
permalink: /docs/describe-construct/
---

Describe is to wrap a set of tests against one functionality; module, structure, set of functions, etc.

The describe construct initializes a test suite. All test suites must begin with a describe construct. Any other constructs outside describe is undefined behavior.

Describe constructs cannot be nested inside another describe. To wrap a set of tests against the functionality under a specific state, use <a href="/docs/context-construct/">context</a> blocks.

#### describe(char* test_suite_description, void test_suite_function_handle(MiniTest*))

If your compiler supports the `__attribute__((constructor))` definition, the `describe` macro accepts the test suite description and function handle.

#### describe(void test_suite_function_handle(MiniTest*))

If your compiler **does not** support the `__attribute__((constructor))` definition, the `describe` macro accepts only the function handle. The test suite description can be passed when the suite is registered in minitest.

```c
minitest.register_suite(&minitest, "test_suite_description", test_suite_function_handle);
```

### Example

```c
{% include examples/constructs/describe/main.c %}
```