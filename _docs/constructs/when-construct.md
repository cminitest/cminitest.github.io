---
title: When
permalink: /docs/when-construct/
---

When wrap a set of tests against the functionality when a specific condition needs to be tested.

#### when(char* condition)

The when construct takes in the condition descriptor `char* condition` and groups a set of tests in its output.

#### Output

```
describe My Test Suite:
  context .add_two_ints
    when the sum does not overflow
      it returns the sum of two numbers
      ...
```

### Example

```c
{% include examples/constructs/when/main.c %}
```