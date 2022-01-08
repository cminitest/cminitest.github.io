---
title: Before
permalink: /docs/fixtures-before/
---

Before fixtures execute in a top-down pattern. The fixture at the highest level of the suite will execute, then those in the current block chain.

Before fixtures execute before each `it` block.

### Example

```c
{% include examples/fixtures/before/main.c %}
```