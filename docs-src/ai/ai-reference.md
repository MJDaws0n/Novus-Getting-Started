# AI reference

This page is the HTML counterpart to the root-level [AI_GUIDE.md](https://github.com/MJDaws0n/Novus-Getting-Started/blob/main/AI_GUIDE.md).

Use the root file when you want a single document for agent ingestion. Use this page when you want the same material inside the docs site.

## Fast rules for AI agents

1. Start from `main.nov` and `libraries.conf`.
2. Check whether imports are aliased or unaliased.
3. Prefer the package loader (`lib/<pkg>/main.nov`) unless the project intentionally imports a specific file.
4. Inspect `#if` blocks before assuming a symbol exists on every platform.
5. If compile errors mention missing functions from a library alias, verify the vendored `lib/<pkg>/` copy is up to date.

## Syntax quick sheet

```novus
module app;

import lib/std std;

fn main() -> i32 {
    let xs: []i32 = [1, 2, 3];
    std.print(std.to_str(std.len(xs)));
    return 0;
}
```

## Builtins worth knowing

- `mov`
- `getreg`
- `syscall`
- `ptr`
- `array_append`
- `len`
- `win_call`

## Package quick sheet

Typical packages in this ecosystem:

- `std`
- `file_io`
- `env`
- `process`
- `window`
- `physics`

## Project references

- [Install Novus and Nox](../guide/install.md)
- [Language Tour](../guide/language-tour.md)
- [Syntax Reference](../reference/syntax-reference.md)
- [Library Reference](../reference/library-reference.md)
- [Inline Assembly](../guide/inline-assembly.md)
- [Working with std](../guide/working-with-std.md)
- [Building the Platformer](../walkthroughs/platformer.md)
- [Building the Todo App](../walkthroughs/todo-app.md)
