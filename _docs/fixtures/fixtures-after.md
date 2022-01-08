---
title: After
permalink: /docs/fixtures-after/
---

After fixtures execute in a bottom-up pattern. The fixture at the lowest level of the suite will execute, then those in the current block execution hierarchy. 

After fixtures execute after each `it` block.

### Example

```c
{% include examples/fixtures/after/main.c %}
```