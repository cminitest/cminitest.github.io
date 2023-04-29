---
title: Output
permalink: /docs/config-output/
---

Minitest supports two outputs: stdio and XML. `minitest.output_format` is to be set prior to executing `minitest.run()`.

---

#### output_format

**Default:** MT_STDIO

**Options:** MT_STDIO, MT_XML

```c
minitest.output_format = MT_XML;
```