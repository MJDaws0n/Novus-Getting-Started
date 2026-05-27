# Syntax reference

This page is the fuller language reference for the syntax you use in real Novus projects.

It is intentionally practical rather than academic: it focuses on the syntax and patterns that appear in the compiler docs, the standard ecosystem libraries, and the example applications linked from this guide.

## Files and modules

Every Novus source file starts with a module declaration:

```novus
module my_app;
```

The root file you compile should define a `main` function. In simple apps that is usually:

```novus
fn main() -> i32 {
    return 0;
}
```

CLI apps may also expose an argument-taking entrypoint:

```novus
fn main(argc: i32, argv: u64) -> i32 {
    return 0;
}
```

## Statement style

Novus code in this ecosystem uses semicolons to end statements:

```novus
let x: i32 = 1;
x = x + 1;
return x;
```

Blocks use braces:

```novus
if (x > 0) {
    print("positive");
}
```

## Comments

Novus documentation describes support for both single-line and block comments:

```novus
// single-line comment

/*
multi-line comment
*/
```

## Types

Novus uses explicit types.

| Type | Meaning |
| --- | --- |
| `i32` | 32-bit signed integer |
| `i64` | 64-bit signed integer |
| `u32` | 32-bit unsigned integer |
| `u64` | 64-bit unsigned integer |
| `f32` | 32-bit floating-point |
| `f64` | 64-bit floating-point |
| `bool` | boolean |
| `str` | string |
| `void` | no return value |
| `[]T` | dynamic array of `T` |

Important rule: there is **no plain `int`**. Use explicit widths like `i32` and `i64`.

## Literals

### Integer literals

```novus
let a: i32 = 0;
let b: i32 = 42;
let c: i64 = 999999999;
```

### Boolean literals

```novus
let ok: bool = true;
let fail: bool = false;
```

### String literals

The ecosystem currently uses string literals heavily. Existing projects show both quoted styles in practice:

```novus
let a: str = "hello";
let b: str = 'world';
```

### Array literals

```novus
let xs: []i32 = [1, 2, 3];
let names: []str = ["Ada", "Max", "Lin"];
let empty: []i32 = [];
```

## Variables

Variables are declared with `let`:

```novus
let count: i32 = 0;
let title: str = "Novus";
```

In current Novus code, variables are mutable:

```novus
let count: i32 = 1;
count = count + 1;
```

Type annotations are written at declaration time:

```novus
let ready: bool = true;
let ids: []i32 = [1, 2, 3];
```

## Global variables

Projects often keep app state in globals:

```novus
let player_x: i32 = 0;
let player_y: i32 = 0;
let app_running: i32 = 1;
```

This pattern is common in current Novus examples, especially where the code is small and explicit state is preferred over abstraction.

## Assignment and update operators

Basic assignment:

```novus
count = 10;
```

Compound assignment:

```novus
count += 1;
count -= 2;
count *= 3;
count /= 4;
count %= 5;
```

Increment / decrement:

```novus
count++;
count--;
```

These are used as statements in current code, not as expression values.

## Functions

Function syntax:

```novus
fn add(a: i32, b: i32) -> i32 {
    return a + b;
}
```

Void-style function:

```novus
fn log_message(msg: str) -> void {
    print(msg);
}
```

### Parameters

Every parameter is typed:

```novus
fn move_player(dx: i32, dy: i32) -> void {
    player_x += dx;
    player_y += dy;
}
```

### Returning values

Use `return`:

```novus
fn max_i32(a: i32, b: i32) -> i32 {
    if (a > b) {
        return a;
    }
    return b;
}
```

### Overloading

Novus supports overloaded functions when the parameter list differs:

```novus
fn show(x: i32) -> void {
    print(i32_to_str(x));
}

fn show(s: str) -> void {
    print(s);
}
```

The return type is not what distinguishes overloads; the parameters do.

## Calls

```novus
let sum: i32 = add(10, 20);
show("ready");
```

## Control flow

### `if`, `else if`, `else`

```novus
if (score > 100) {
    print("high");
} else if (score > 50) {
    print("mid");
} else {
    print("low");
}
```

### `while`

```novus
let i: i32 = 0;
while (i < 10) {
    print(i32_to_str(i));
    i += 1;
}
```

Current examples rely heavily on `while`.

## Operators

### Arithmetic

- `+`
- `-`
- `*`
- `/`
- `%`

### Comparison

- `==`
- `!=`
- `<`
- `<=`
- `>`
- `>=`

### Logical

- `&&`
- `||`
- `!`

### Bitwise

Current library and application code also uses bitwise operators for things like input masks:

- `&`
- `|`

Example:

```novus
if ((input_mask & window.wm_input_quit()) != 0) {
    app_running = 0;
}
```

## Strings

Strings are used heavily across the ecosystem.

### Concatenation

```novus
let msg: str = "Hello " + name;
```

### Indexing

Projects index strings directly:

```novus
if (line[i] == ' ') {
    ...
}
```

### Common string patterns

You will often see:

- `len(s)`
- `substr(...)`
- `substr_len(...)`
- `str_find(...)`
- conversion helpers from `std`

Some of these are builtin patterns, others come from `std`.

## Arrays

### Declaration

```novus
let xs: []i32 = [10, 20, 30];
```

### Indexing

```novus
let first: i32 = xs[0];
```

### Append

```novus
array_append(xs, 40);
```

### Empty arrays

```novus
let names: []str = [];
```

## Imports

Common import forms:

### Alias import

```novus
import lib/std std;
import lib/window/main window;
```

### Unaliased import

```novus
import lib/std;
```

That brings exported names directly into the current module.

### Package entrypoints

Modern Novus libraries usually expose a stable `main.nov` loader. That is why imports such as these are common:

```novus
import lib/process/main process;
import lib/file_io fio;
```

## Conditional compilation

Novus uses `#if(...)` to include platform-specific code at compile time.

### OS selection

```novus
#if(os == "darwin") {
    import platforms/darwin/arm64;
}

#if(os == "linux") {
    import platforms/linux/common;
}

#if(os == "windows") {
    import platforms/windows/common;
}
```

### Architecture selection

```novus
#if(arch == "arm64") {
    import arm64;
}

#if(arch == "amd64") {
    import amd64;
}
```

The most common conditions in the current ecosystem are:

- `os == "darwin"`
- `os == "linux"`
- `os == "windows"`
- `arch == "arm64"`
- `arch == "amd64"`
- `arch == "x86"`

## Builtins

Common compiler-provided builtins:

- `len(...)`
- `array_append(...)`
- `ptr(...)`
- `mov(...)`
- `getreg(...)`
- `syscall()`
- `push(...)`
- `pop()`
- `win_call(...)`

These do not require imports.

## Low-level syntax

Low-level Novus libraries use register operations directly:

```novus
mov(x0, fd);
mov(x1, ptr(buf));
mov(x2, len(buf));
mov(x16, 0x2000000 + 4);
syscall();
let rc: u64 = getreg(x0);
```

Windows-specific wrappers often use:

```novus
win_call("ExitProcess", 0);
```

## Program entrypoints

You will see two main styles:

### Simple program

```novus
fn main() -> i32 {
    return 0;
}
```

### CLI program

```novus
fn main(argc: i32, argv: u64) -> i32 {
    if (argc <= 1) {
        return 1;
    }
    return 0;
}
```

## CLI usage

Typical compiler command:

```bash
novus main.nov
```

Cross-compile:

```bash
novus --target=linux/amd64 main.nov
```

Build artifacts are written into `build/<target>/`.

## Nox project syntax in practice

Typical project flow:

```bash
nox init my-project
cd my-project
nox pull window
novus main.nov
```

That gives you:

- `main.nov`
- `libraries.conf`
- `lib/<package>/...`

## Practical style notes

Current Novus projects in this ecosystem generally follow these conventions:

1. use explicit integer sizes (`i32`, `i64`)
2. prefer alias imports for larger libraries
3. use `main.nov` as the package entrypoint
4. keep cross-platform branching in libraries via `#if`, not in app code when possible
5. use explicit loops and explicit state rather than heavy abstraction

## Where to go next

- For a quicker introduction, go back to the [Language Tour](../guide/language-tour.md).
- For real code, read the [Platformer walkthrough](../walkthroughs/platformer.md) and [Todo app walkthrough](../walkthroughs/todo-app.md).
- For package surfaces, use the [Library Reference overview](library-reference.md).

