# Novus, from zero to real projects

This guide walks through **installing Novus and Nox**, creating a project, using `std`, writing inline assembly, and understanding how real Novus projects are structured.

## What this repo covers

- [First project](guide/first-project.md) — from `nox init` to your first compiled binary
- [Language tour](guide/language-tour.md) — modules, imports, functions, arrays, strings, overloads, and `#if`
- [Inline assembly](guide/inline-assembly.md) — `mov`, `getreg`, `syscall`, and `win_call`
- [Working with std](guide/working-with-std.md) — standard library usage and common patterns
- [Platformer walkthrough](walkthroughs/platformer.md) — rendering loop, input handling, camera, and window API
- [Todo app walkthrough](walkthroughs/todo-app.md) — a simple CLI app with file-backed storage

!!! note "Compatibility snapshot"
    These docs were written against the currently installed toolchain on this machine:

    - **Novus compiler:** `V0.2.0`
    - **Novus repo:** `753ee3c`
    - **Nox repo:** `632c8be`
    - **window library:** `1.1.1`
    - **std examples:** based on current ecosystem usage in the linked repos

## Recommended reading order

1. [Install Novus and Nox](guide/install.md)
1. [Install Novus and Nox](guide/install.md)
2. [Your First Project](guide/first-project.md)
3. [Language Tour](guide/language-tour.md)
4. [Working with std](guide/working-with-std.md)
5. [Nox and Libraries](guide/nox-and-libraries.md)
6. [Inline Assembly](guide/inline-assembly.md)
7. Project walkthroughs

## When to use the AI docs

If you are building tooling, generating Novus code automatically, or teaching an AI agent how to reason about a Novus repo, start with:

- [AI reference](ai/ai-reference.md)
- root-level [AI_GUIDE.md](https://github.com/MJDaws0n/Novus-Getting-Started/blob/main/AI_GUIDE.md)
- root-level [llms.txt](https://github.com/MJDaws0n/Novus-Getting-Started/blob/main/llms.txt)

## Related repositories

- [Novus](https://github.com/MJDaws0n/Novus)
- [Nox](https://github.com/MJDaws0n/Nox)
- [Todo-App](https://github.com/MJDaws0n/Todo-App)
- [platformer-game](https://github.com/MJDaws0n/platformer-game)
