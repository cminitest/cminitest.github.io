---
title: It
permalink: /docs/it-construct/
---

It constructs contain the assertion for the current test scenario. They can be scoped to any construct.

**Note:** all assertions must be in an it block. The assertion will run, but will not be included in the output summary.

#### it(char* description)

The it construct takes in the description of an assertion to reflect what is being tested.

#### Output

```
describe My Test Suite:
  context .add_two_ints
    it returns the sum of two numbers
    when the sum overflows
      it returns 0
        ...
```

### Example

```c
{% include examples/constructs/it/main.c %}
```