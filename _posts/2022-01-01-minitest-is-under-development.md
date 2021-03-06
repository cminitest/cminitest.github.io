---
layout: post
title:  "Case Study: Minitest"
date:   2022-01-01 11:11:11
author: Benjamin J. Anderson
summary: "Minitest, a behavior-driven test library for C, is under development."
---

**C** is an amazing programming language. At its core, it's a small, but effective. If you want to write programs for a microprocessor, embedded system, windows, solaris, darwin(mac), linux, unix -- just about anything -- **C** will run. The problem is there are many compilers and variations ("extensions") to the **C** language. There are excellent test frameworks out there for C, but many require more than the ISO C11-17 standard; sometimes even a C++ compiler. Others are minimalistic and don't serve the complex reporting needed for larger systems. The majority are explicit with assertions and can be a challenge for introducing new developers to a large codebase with many unique data types.

### Case Study

---

*Disclaimer:* There is nothing incorrect with explicit assertions and the styling with **C** unit test libraries. Explicit syntax reduces confusion on what an assertion is doing behind the scenes. The downside is it introduces on-boarding overhead and "guessing" game on what assertion function to use for a particular data type.

---

With many **C** unit testing libraries assertions are a set of functions that compare a data type and return a value. This value, usually a boolean, is then registered to the test framework result -- true being it passed, false being it failed.

```c
int assert_int_equals(int actual, int expected) {
  return actual == expected;
}

int assert_int_less_than(int actual, int expected) {
  return actual < expected;
}

/* etc.. */
```

The developer will define a test case and assert their function gives the expected value.

```c
TEST_CASE(add_returns_the_sum_of_two_numbers) {
  return assert_int_equals(add(2,2), 4);
}
```

This test case is then registered to the test suite.

```c
int main(void) {
  TestCase testsuite[] = { add_returns_the_sum_of_two_numbers };
  run_test_suite(testsuite);
}
```

For core **C** data types, these assertion functions are predictable and follow a convention. These assertions will be defined as 

`assert_<data type>_condition`.

Complex data types, such as arrays, may be defined as

`assert_<data type>_array_condition(a[], e[], size_t a, size_t e)`.

Eventually the codebase will grow in complexity and more custom data types will be defined. For each data type, an assertion function for the type and possibly the array form will be defined.

```c
typedef struct LinkedListStruct {
  int size;
  ListElement *head;
} LinkedList;

int assert_linked_list_equals(LinkedList *actual, LinkedList *expected);
```

For these custom data types, the development team will have to enforce conventions on assertions. Will it be underscored or camel-case? For pointer types will it be defined as `assert_<data type>_ptr_<condition>` or `assert_<data type>_pointer_<condition>`? A developer who has been on the team awhile will understand these conventions and possibly know all the assertion functions for the project. A new developer may be able to guess the assertion function, but will often need to refer to documentation/code to effectively write tests for their commits.

### Introducing Minitest

Minitest aims to reduce the assertion complexity and test setup through macros that drive the test library. This offers an elegant and consistent syntax across the test suite. Consistency reduces overhead and the time required to onboard new developers.

For example, in Minitest, a test suite can be defined like so:

```c
#include "minitest/minitest.h"

describe("CustomMathLib", custom_math_lib)
  context("add")
    it("returns the sum of two integers")
      expect(add(2,2)) to equal(4)
    end
  end
end

int main() {
  minitest.output_format = MT_STDIO;
  minitest.run();

  int failures = minitest.failures;

  minitest.clear(&minitest);
  return failures > 0 ? 1 : 0;
}
```

Incorporating the LinkedList example, we need a custom assertion to verify if two lists are equal. In Minitest, you can define custom assertions without any modifications to the assertion syntax.

```c
//
// extension.h
//
#define MT_EXPECT_EXT \
  mt_register_expect_extension(linked_list, LinkedList*)

#include "minitest/minitest.h"

mt_expect_forward(linked_list,  LinkedList*);

//
// extension.c
//

// for brevity, check only the size of the linked lists
mt_expect_ext_default(linked_list, LinkedList*, (actual->size == expected->size), NULL);
```

The definition of `MT_EXPECT_EXT` inserts a function call and type check to C11's _Generic definition for the expect() macro. This creates an expectation for the LinkedList* type and reference to the forwarded function generated by the `mt_expect_forward` macro. Through this extension, we can now do assetions against our LinkedList* type.

```c
#include "extension.h"

describe("LinkedList", linked_list)
  LinkedList users;
  users.size = 1;

  when("two linked lists are compared")
    LinkedList compared_users;

    and("the linked list sizes are equal")
      compared_users.size = 1;
      it("asserts the list sizes are equal")
        expect(&users) to equal(&compared_users)
      end
    end

    and("the linked list sizes are not equal")
      compared_users.size = 0;
      it("asserts the list sizes are not equal")
        expect(&users) to not equal(&compared_users)
      end
    end
  end
end
```

### Conclusions

Minitest requires additional *setup* overhead in contrast to most testing libraries. Once configured and assertions are defined for custom data types, there is no guesswork. The testing syntax is consistent across all test suites. Test suites do not need to be registered (if the compiler supports `__attribute__((constructor))` -- *describe* has a slightly different syntax if not). This compromise for consistency and reduced on-boarding overhead is the core of Minitest's mission.

