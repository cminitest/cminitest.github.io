---
title: Logging
permalink: /docs/config-logging/
---

Minitest logging offers DEVELOPMENT, FATAL. ERROR, WARN, INFO, and DEBUG logs. These logs offer insights into the internal state of Minitest and its assertions. `minitest.log_level` is to be set prior to executing `minitest.run()`.

---

#### log_level

**Default:** MT_LOG_NONE

**Options:** MT_LOG_NONE, MT_LOG_DEVELOPMENT, MT_LOG_FATAL, MT_LOG_ERROR, MT_LOG_WARN, MT_LOG_INFO, MT_LOG_DEBUG, MT_LOG_ALL 

Log output level from minitest.