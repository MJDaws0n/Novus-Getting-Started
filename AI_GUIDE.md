# AI Documentation: Novus and Nox

This file is written **for AI agents**.

Use it when you need a compact but accurate operational model of the Novus ecosystem: language syntax, imports, packaging, inline assembly, conditional compilation, and the most common project patterns.

## What Novus is

Novus is a small statically typed systems language that compiles directly to native binaries. Current project material in this ecosystem targets:

- `darwin/arm64`
- `linux/amd64`
- `linux/arm64`
- `linux/386`
- `windows/amd64`

The compiler writes artifacts into `build/<target>/`.

Typical command:

```bash
novus main.nov
```

Cross compile:

```bash
novus --target=linux/amd64 main.nov
```

## Project structure

A typical Nox-managed Novus project looks like this:

```text
my-project/
├── main.nov
├── libraries.conf
└── lib/
    ├── std/
    ├── file_io/
    └── window/
```

Important points:

- `lib/<package>/main.nov` is the normal package entrypoint.
- Many official libraries use platform dispatch loaders in `main.nov`.
- Packages may also expose internal files like `lib/std/main`, but user-facing code should normally import the package entrypoint or the documented file path.

## Nox model

Use Nox to initialise and populate projects:

```bash
nox init my-project
cd my-project
nox pull window
```

Modern `libraries.conf` files may look like:

```conf
installed=std,file_io

pkg:std:source=registry
pkg:std:url=https://github.com/MJDaws0n/novus-std
pkg:std:version=1.3.0
```

Legacy projects may still include `branch=` and `commit=` lines. If a local `lib/` directory is stale, a project can compile against old package code even when the upstream registry has moved on.

## Core syntax

### Modules

```novus
module my_app;
```

### Imports

Alias import:

```novus
import lib/std std;
```

Explicit file import:

```novus
import lib/window/main window;
```

No alias:

```novus
import lib/std;
```

No-alias imports bring names directly into the current module. Prefer aliases unless the library documentation explicitly expects otherwise.

### Functions

```novus
fn greet(name: str) -> void {
    print("Hello " + name);
}
```

Novus supports function overloading when signatures differ:

```novus
fn greet(name: str) -> void { print("Hi " + name); }
fn greet(times: i32) -> void { print(i32_to_str(times)); }
```

### Variables and types

```novus
let name: str = "Max";
let count: i32 = 3;
let big: i64 = 99;
let ok: bool = true;
let xs: []i32 = [1, 2, 3];
```

### Control flow

```novus
if (count > 0) {
    print("positive");
}

while (count > 0) {
    count = count - 1;
}
```

## Common builtins

Language builtins commonly used in normal user code:

- `len(str) -> i32`
- `array_append(xs, v)`
- `ptr(value) -> u64`

Low-level builtins commonly used in systems libraries:

- `mov(reg, value)`
- `getreg(reg) -> u64`
- `syscall()`
- `push(value)`
- `pop() -> u64`
- `win_call("FunctionName", args...)`

Typical raw syscall pattern:

```novus
mov(x0, fd);
mov(x1, ptr(buf));
mov(x2, len(buf));
mov(x16, 0x2000000 + 4);
syscall();
let rc: u64 = getreg(x0);
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

#if(arch == "amd64") {
    import amd64;
}
```

Observed conditions in this ecosystem:

- `os == "darwin"`
- `os == "linux"`
- `os == "windows"`
- `arch == "arm64"`
- `arch == "amd64"`
- `arch == "x86"`

Use `#if` in platform loader modules and low-level libraries.

## Standard library expectations

`std` is the first library most projects use. Common patterns:

```novus
import lib/std std;

fn main() -> i32 {
    std.print("Hello");
    let xs: []i32 = [1, 2, 3];
    std.print(std.to_str(std.len(xs)));
    std.exit(0);
    return 0;
}
```

Important conventions in the modern ecosystem:

- Prefer unified helper names like `len(...)` and `to_str(...)`.
- Prefer explicit integer types like `i32` and `i64`.
- Official libraries usually expose a stable `main.nov` loader.

## Window library notes

The `window` package exposes `wm_*` functions such as:

- `wm_open_default`
- `wm_resize`
- `wm_size`
- `wm_input`
- `wm_clear`
- `wm_rect`
- `wm_present`
- `wm_quit`

Input bit helpers:

- `wm_input_left()`
- `wm_input_right()`
- `wm_input_jump()`
- `wm_input_down()`
- `wm_input_quit()`

On current macOS builds, `wm_size(fd)` is expected to reflect the live content size of the Cocoa window, so apps can react to user-driven resizes.

## Package authoring rules

When generating or editing a Novus package:

1. Put the public loader in `main.nov`.
2. Use platform folders if the package has OS/arch-specific code.
3. Keep tests grouped in `tests/` or equivalent documented layout.
4. Keep a `VERSION` file for publishable packages.
5. Keep `libraries.conf` accurate for downstream dependency resolution.

## Useful commands

```bash
nox init my-app
nox pull std
nox pull file_io
nox pull window
novus main.nov
novus --target=linux/amd64 main.nov
```

## Common pitfalls

1. **Stale vendored packages**: local `lib/` contents can lag behind the registry and cause confusing compile errors.
2. **Mixed import styles**: some older projects use `import lib/std;`, while newer ones prefer alias imports.
3. **Platform-specific loaders**: a package may compile on one OS and fail on another if its `#if` loader is incomplete.
4. **Inline assembly docs**: many advanced patterns live in library code and legacy docs rather than the short README.
5. **Old project code**: when documenting or refactoring older projects, check whether they predate the current library layout.

## Best references

- Novus repo: <https://github.com/MJDaws0n/Novus>
- Nox repo: <https://github.com/MJDaws0n/Nox>
- Todo-App: <https://github.com/MJDaws0n/Todo-App>
- Platformer: <https://github.com/MJDaws0n/platformer-game>
- Human docs site: <https://mjdaws0n.github.io/Novus-Getting-Started/>

