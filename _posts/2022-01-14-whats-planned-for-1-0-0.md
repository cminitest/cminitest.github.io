---
layout: post
title:  "What's Planned for 1.0.0"
date:   2022-01-14 09:00:00
author: Benjamin J. Anderson
summary: "Minitest is approaching 1.0.0 with some major changes. Learn more about what's planned."
---

Minitest is under a proof-of-concept phase. Assertions, syntax, extensions have examples and Minitest is tested with Minitest. At its core, Minitest has *most* of the functionality required out of a unit testing library. Its syntax is elegant and predictable. Behind the scenes Minitest needs some work. Here's what's coming to Minitest in its 1.0.0 release!

### More verboseness with undefined behaviors

Minitest doesn't offer much assistance to new C developers or those wanting to use Minitest. There are plenty of examples, but a typo in the assertion syntax or a construct can print out less-than optimal macro expansion stack traces. When there's an undefined behavior, Minitest terminates:

```c
if (!mt->current) {
  return;
}
```

This will change with a logging interface that can be enabled or disabled through arguments to the test suite.

### "mt_" prefixed macros

Minitest is driven by macros. Much of the codebase is building a list of nodes and collecting the assertion results. To prevent conflicts with other libraries developers are using, all macros must be prefixed with "mt_". Constructs and assertion macros will not have the syntax prefixed.

### Mocking

The current mocking interface and functionality is limited to specifying a return value and tracking the number of times the mock was called. Minitest wants to take this a step further and track each individual call, the arguments, and returned results (if any).

Mocking with C is a challenge to cover all scenarios. Functions can return values or modify a parameter. Being able to accommodate this functionality is possibly beyond the scope of Minitest and can be addressed with architecting in a way that can be better tested.

Mocking and asserting a call was called with arguments is something Minitest will include. Asserting a function was called doesn't provide enough context to the state of the caller. To handle this context, Minitest will have to change its mocking syntax.

This is not a final syntax as refactoring the mock syntax is being reviewed.

```c
//
// mock.h
//

mt_mock_forwards(function_ptr, return_type, arg_count, arg_type arg_name1 ...);

//
// mock.c
//

// void function
mock(void_function) with any_args no_return

// non-void function
mock(add_two_ints) with args(2,2) and_return(5)
```

Prior to forwarding your mock and similar to the extensions interface, a constant will have to be defined to check if the parameter type matches a custom data type and registration into a union of values.

### Licensing and Community Guidelines

Prior to the 1.0.0 release, Minitest will be released under the MIT 2.0 license. There will also be guidelines in the README of the project specifying how to contribute and reach out to the community.

