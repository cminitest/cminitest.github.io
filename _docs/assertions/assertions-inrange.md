---
title: In Range
permalink: /docs/assertions-inrange/
---

The in_range assertion checks if the expected numeric value is greater than or equal to the lower bound, and less than or equal to the upper bound.

**Note:** Behavior is undefined in the context of an array.

### Example

```c
{% include examples/assertions/inrange/main.c %}
```