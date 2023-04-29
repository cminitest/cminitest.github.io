---
title: Overview
permalink: /docs/signals-overview/
---

Minitest can be configured to capture signals in assertion (`it`) blocks. SIGABRT, SIGFPE, SIGILL, SIGINT, SIGSEGV, SIGTERM are supported. To capture a signal, or multiple signals, `minitest.signals` is to be set prior to `minitest.run`. To add multiple signals, chain a bitwise `or` for each signal.

Each signal is prefixed with `MT_` for chaining. Example: `MT_SIGFPE`, `MT_SIGSEGV`, etc. When a signal is captured, Minitest will report the error in the test suite with the signal number and continue execution.

---

#### Example

```c
minitest.signals = MT_SIGFPE | MT_SIGSEGV;
minitest.run();
```

##### Result

```
 describe  MiniTest:
    context  Signals
      when  a signal is captured
        ✖ it reports the error 
        Expected (Signal) to not have been captured (11) 
      when  the signal was captured
        ✔ it runs the next test 
```