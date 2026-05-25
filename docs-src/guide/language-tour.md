# Language tour

This page is a practical tour of the syntax you actually see in Novus projects.

## Modules and imports

```novus
module example;

import lib/std std;
import lib/window/main window;
```

## Variables and basic types

```novus
let name: str = "Novus";
let count: i32 = 3;
let big: i64 = 999999;
let ready: bool = true;
```

The ecosystem strongly prefers explicit integer sizes like `i32` and `i64`.

## Functions

```novus
fn greet(name: str) -> void {
    print("Hello " + name);
}
```

Functions can return values:

```novus
fn add(a: i32, b: i32) -> i32 {
    return a + b;
}
```

## Overloading

Novus supports function overloading when parameter types differ.

```novus
fn label(value: i32) -> str {
    return "number";
}

fn label(value: str) -> str {
    return "text";
}
```

## Conditionals

```novus
if (count > 0) {
    print("positive");
}
```

## Loops

```novus
let i: i32 = 0;
while (i < 3) {
    print("loop");
    i = i + 1;
}
```

## Strings

```novus
let msg: str = "Hello";
let joined: str = msg + " world";
let size: i32 = len(joined);
```

## Arrays

```novus
let xs: []i32 = [10, 20, 30];
array_append(xs, 40);
let first: i32 = xs[0];
```

## Conditional compilation

Novus uses `#if(...)` for compile-time platform selection.

```novus
#if(os == "darwin") {
    import platforms/darwin/arm64;
}

#if(os == "linux") {
    import platforms/linux/common;
}
```

You will see this constantly in official libraries.

### Common conditions

- `#if(os == "darwin")`
- `#if(os == "linux")`
- `#if(os == "windows")`
- `#if(arch == "arm64")`
- `#if(arch == "amd64")`
- `#if(arch == "x86")`

## Builtins versus libraries

Some things are compiler builtins:

- `len`
- `array_append`
- `mov`
- `getreg`
- `syscall`
- `ptr`

Most everyday work should still go through libraries such as `std`, `file_io`, `window`, `net`, or `physics`.

## A complete small example

```novus
module example;

import lib/std std;

fn describe(value: i32) -> str {
    return "number " + std.to_str(value);
}

fn describe(value: str) -> str {
    return "text " + value;
}

fn main() -> i32 {
    let xs: []i32 = [1, 2, 3];
    std.print(describe(std.len(xs)));
    std.print(describe("ready"));
    std.exit(0);
    return 0;
}
```

