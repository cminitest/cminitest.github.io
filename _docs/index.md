---
title: Overview
permalink: /docs/home/
redirect_from: /docs/index.html
---

<style>
  ul.badges { list-style-type: none; margin: 0; padding: 0; margin-bottom: 1em; }
  ul.badges li { display: inline-block; }
</style>

<ul class="badges">
  <li><img src="https://github.com/cminitest/minitest/actions/workflows/MacOS.yml/badge.svg"/></li>
  <li><img src="https://github.com/cminitest/minitest/actions/workflows/Windows.yml/badge.svg"/></li>
  <li><img src="https://github.com/cminitest/minitest/actions/workflows/Ubuntu.yml/badge.svg"/></li>
</ul>

## Goals

- A small, behavior-driven, test library for C.
- No extensions to the C-library
- Extensible assertions

## Functionality

- An elegant syntax
- A variety of default assertions
- Signal Capturing
- Extensible
- Configurable Output Formats

## Example

```c
#include "minitest/minitest.h"

describe("MiniTest", minitest_suite)
  it("is defined")
    expect(&minitest) to equal(&minitest)
  end
  
  context(".register_block")
    when("a block has not had any it blocks defined")
      it("creates a new array with 1 element")
        minitest.register_block(IT_TYPE, &minitest, "it block test");
        expect(minitest.current->it_blocks.size) to equal(1);
      end
    end
  end
end

int main() {
  minitest.run();
  int failures = minitest.failures;
  minitest.clear(&minitest); // optional, frees memory and clears the test suite
  return failures > 0 ? 1 : 0;
}
```

### Output

```
describe Minitest:
  ✔ it is defined
  context .register_block
    when a block has not had any it blocks defined
      ✔ it creates a new array with 1 element
```
