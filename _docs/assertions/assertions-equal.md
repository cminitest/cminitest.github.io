---
title: Equal
permalink: /docs/assertions-equal/
---

The equal assertion checks if two values are equal.

In the context of an array, the assertion performs a `qsort` after asserting the lengths of the arrays are equal. Each value in the array is then compared.

### Example

```c
{% include examples/assertions/equal/main.c %}
```