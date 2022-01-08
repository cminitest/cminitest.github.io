---
title: Be False
permalink: /docs/assertions-be-false/
---

The be_false assertion checks if the expected value is equal to 0.

**Note:** this is not `stdbool.h` and uses integer representation for booleans.

**Note:** Behavior is undefined in the context of an array.

### Example

```c
{% include examples/assertions/befalse/main.c %}
```