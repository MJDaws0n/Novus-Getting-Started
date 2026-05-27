# Working with std

--8<-- "includes/status-warning.md"


The standard library is the package almost every Novus project touches first.

## Import style

The cleanest modern pattern is:

```novus
import lib/std std;
```

In some projects you may also see:

```novus
import lib/std/main;
```

Both styles exist in the current ecosystem. When in doubt, check the package entrypoint in `lib/std/main.nov`.

## Useful patterns

### Printing

```novus
std.print("hello");
```

### Converting values

```novus
let count: i32 = 5;
std.print(std.to_str(count));
```

### Length helpers

```novus
let text: str = "abc";
let xs: []i32 = [1, 2, 3];

std.print(std.to_str(std.len(text)));
std.print(std.to_str(std.len(xs)));
```

### Strings and arrays

Novus applications often combine builtins and std-style helpers:

```novus
let xs: []str = [];
array_append(xs, "first");
array_append(xs, "second");
std.print(std.to_str(std.len(xs)));
```

## Why std matters

`std` is where application code should start before reaching for inline assembly or platform-specific packages.

It lets you:

- print and exit cleanly
- convert numbers to strings
- work with arrays and strings idiomatically
- avoid re-implementing basic helpers in every project

## Example

```novus
module hello_std;

import lib/std std;

fn main() -> i32 {
    let title: str = "Novus";
    let nums: []i32 = [4, 8, 15, 16];

    std.print("Title: " + title);
    std.print("Items: " + std.to_str(std.len(nums)));
    std.exit(0);
    return 0;
}
```

## Real-world note

Older projects may still call helpers like `array_len_str(...)` or use broad unaliased imports. Modern docs and modern libraries are moving toward a more consistent surface where common operations are unified.

