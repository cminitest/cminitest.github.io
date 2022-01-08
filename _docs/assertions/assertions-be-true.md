---
title: Be True
permalink: /docs/assertions-be-true/
---

The be_true assertion checks if the expected value equal to 1.

**Note:** this is not `stdbool.h` and uses integer representation for booleans.

**Note:** Behavior is undefined in the context of an array.

### Example

```c
{% include examples/assertions/betrue/main.c %}
```