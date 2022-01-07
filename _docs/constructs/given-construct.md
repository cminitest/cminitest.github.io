---
title: Given
permalink: /docs/given-construct/
---

A behavior-style alias for <a href="/docs/when-construct">when</a>.

#### Output

```
describe My Test Suite:
  context .add_two_ints
    given the sum does not overflow
      it returns the sum of two numbers
      ...
```

### Example

```c
{% include examples/constructs/given/main.c %}
```