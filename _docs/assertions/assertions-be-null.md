---
title: Be NULL
permalink: /docs/assertions-be-null/
---

The be_null assertion checks if a void pointer is equal to NULL.

**Note:** Behavior is undefined in the context of an array.

### Example

```c
{% include examples/assertions/benull/main.c %}
```