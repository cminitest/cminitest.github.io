---
title: Mocking
permalink: /docs/mocks-mocking/
---

Mocking simulates a function to trigger a specific state in your application. This is often in situations involving File IO and socket connections/networking.

### "Don't mock what you don't own"

"Don't mock what you don't own" is a phrase you'll often hear when working with mocks. This gives mocking a negative light and can deter developers from using them. When you hear this feedback, it involves mocking out the real thing. The following example mocks out C's native `getline` function and returns the number of characters read.


```c
mock(getline) and_return(10)
```

This often triggers the don't mock what you don't own discussion. When you hear this phrase, it's **not** feedback on testing, it's feedback on the **design** of your application to support unit testing. To better support tests, and mocking, you should wrap any functions you don't own with a function that supports and describes the process.

```c
char* read_transaction(FILE* fp) {
  char* buffer = NULL;
  size_t buffer_size = 0;

  getline(&buffer, &buffer_size, fp);

  return buffer;
}
```

We can then mock the `read_transaction` function and provide supporting tests (with or without mocking).

```c
mock(read_transaction) and_return("I'm a line in a file")
```

### Macros

Minitest includes the following macros to support mocking in a unit test suite.

#### mock(function_pointer) and_return(return_value)

Mock registers a new mock in the test suite for the function `function_pointer`. When calling the mock, it will return the value specified in `and_return(return_value)`. 

#### release_mock(function_pointer)

`release_mock` releases the mock from any future calls. All calls will point to tge `__real_<function_name>` function.

#### mock_calls(function_pointer)

Gets the number of times the mock was called. This returns an integer. 

### Example

**Library.c**

```c
{% include examples/assertions/beencalled/lib.c %}
```

**main.c**

```c
{% include examples/assertions/beencalled/main.c %}
```