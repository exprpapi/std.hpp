# std.hpp
Import C++23 Standard Library by default

## Rationale
Precompile this header, and include it instead of any other C++23stdlib headers.
There is no reason at all to manually include headers.
It is tedious, error-prone and compiles much slower than simply including a precompiled header, which compiles instantly.
Additionally, modern compilers can discard unused includes, if binary size is of issue.

## Installation
Locate your include path, in my case: `LOCAL_INCLUDE=${HOME}/.local/include/`.  
Emplace the header: `${LOCAL_INCLUDE}/std/std.hpp`.

## Example Usage
Using your compile command, in my case: `CPP_CMD=(g++ --std=c++2b -g -Wall -Wextra -Wpedantic)` precompile the header, and compile programs using that header like:
```bash
$ ${CPP_CMD} "${LOCAL_INCLUDE}/std/std.hpp"
$ ${CPP_CMD} -I"${LOCAL_INCLUDE}/std" example.cpp -o example
$ ./example first_argument second_argument
0: ./example
1: first_argument
2: second_argument
```

where
```C++
// example.cpp
#include <std.hpp>

auto print(auto... args) {
  (std::cout << ... << args) << std::endl;
}

auto main(int argc, char** argv) -> int {
  auto args = std::vector<std::string>(argv, argv + argc);
  auto i = 0;
  for (auto arg : args) {
    print(i++, ": ", arg);
  }
}
```
