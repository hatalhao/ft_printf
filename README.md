# ft_printf

A lightweight, 42-style reimplementation of the C standard library's `printf`, written in C and built as a static library.

This project provides a drop-in function `ft_printf` with a subset of standard `printf` features commonly required in the 42 curriculum.

- Language: C
- Build system: Makefile

## Features

- Function signature:
  ```c
  int ft_printf(const char *format, ...);
  ```
- Returns the number of characters printed.
- Writes to standard output (file descriptor 1).
- Supported conversion specifiers:
  - `%c` — character
  - `%s` — string
  - `%p` — pointer (hexadecimal with `0x` prefix)
  - `%d`, `%i` — signed decimal integer
  - `%u` — unsigned decimal integer
  - `%x` — unsigned hexadecimal (lowercase)
  - `%X` — unsigned hexadecimal (uppercase)
  - `%%` — literal percent sign

## Getting Started

### Prerequisites
- A C toolchain (e.g., `gcc` or `clang`)
- `make`

### Build

From the project root:
```sh
make
```

Common Makefile targets:
- `make` — build the library
- `make clean` — remove object files
- `make fclean` — remove objects and the library
- `make re` — rebuild from scratch

### Using ft_printf in your project

1. Include the header in your source:
   ```c
   #include "ft_printf.h"
   ```

2. Compile and link against the static library. Example:
   ```sh
   gcc -Wall -Wextra -Werror -I./include -c main.c
   gcc -o app main.o -L. -lftprintf
   # or simply
   gcc -Wall -Wextra -Werror main.c ./libftprintf.a -I./include
   ```

### Minimal example

```c
#include "ft_printf.h"

int main(void)
{
    int printed = ft_printf("Hello, %s! Number: %d Hex: %x %%\n", "world", 42, 0x2A);
    ft_printf("Characters printed above: %d\n", printed);
    return 0;
}
```

Build:
```sh
gcc -Wall -Wextra -Werror main.c ./libftprintf.a -I./include -o demo
./demo
```

## Behavior Notes

- The return value accumulates the count of characters successfully written.
- Pointer values are printed with a `0x` prefix followed by lowercase hexadecimal digits.

## Testing

Quick comparison test:
```c
int a = ft_printf("Mine => %d %x %p %%\n", 42, 42, &a);
int b = printf   ("Sys  => %d %x %p %%\n", 42, 42, &a);
printf("ft_printf count: %d | printf count: %d\n", a, b);
```

Compile:
```sh
gcc -Wall -Wextra -Werror test.c ./libftprintf.a -I./include -o test
./test
```

## Development Guidelines

- Compile with `-Wall -Wextra -Werror`.
- Keep functions small and focused on a single conversion responsibility.
- Consider adding internal helper functions for hexadecimal and pointer formatting.
