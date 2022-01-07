---
title: And
permalink: /docs/and-construct/
---

And constructs expand the current testing scenario, groups tests that assert the conditions.

#### and(char* condition)

The and construct takes in the condition descriptor `char* condition` and groups a set of tests in its output.

#### Output

```
describe My Test Suite:
  context .add_two_ints
    when the sum does not overflow
      and both number are not negative
        it returns the sum of two numbers
        ...
```

### Example

```c
{% include examples/constructs/and/main.c %}
```