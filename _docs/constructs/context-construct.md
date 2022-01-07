---
title: Context
permalink: /docs/context-construct/
---

Contexts wrap a set of tests against the functionality under a specific state. This can be a specific function or subject. 

#### context(char* context)

The context construct takes in the current context descriptor `char* context` and groups a set of tests in its output.

#### Output

```
describe My Test Suite:
  context .add_two_ints
    it returns the sum of two numbers
      ...
```

### Example

```c
{% include examples/constructs/context/main.c %}
```