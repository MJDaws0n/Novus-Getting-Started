# Inline assembly

One of the distinctive parts of Novus is that low-level work happens inside the language rather than through a separate FFI layer for every platform.

This is mainly useful for:

- syscalls
- register manipulation
- tiny platform backends
- Windows API calls via `win_call`

Most application code should still prefer `std` and existing libraries.

## The core builtins

| Builtin | What it does |
| --- | --- |
| `mov(reg, value)` | load a value into a register |
| `getreg(reg)` | read a register value |
| `syscall()` | issue a syscall on Unix-like targets |
| `ptr(value)` | get the address of a value |
| `push(value)` / `pop()` | direct stack operations |
| `win_call("Name", ...)` | call a Windows API symbol |

## A tiny register example

```novus
fn read_back_demo() -> u64 {
    mov(x0, 42);
    return getreg(x0);
}
```

This does not do any OS work. It just proves that Novus can place and read values directly from registers.

## A syscall-shaped example

The exact syscall numbers are platform-specific, but the structure is always the same:

```novus
fn raw_write(fd: i32, buf: str) -> u64 {
    mov(x0, fd);
    mov(x1, ptr(buf));
    mov(x2, len(buf));
    mov(x16, 0x2000000 + 4);
    syscall();
    return getreg(x0);
}
```

That is the general pattern used in many Novus low-level libraries:

1. load arguments into the correct registers
2. load the syscall number
3. call `syscall()`
4. read the result with `getreg(...)`

## Windows API calls

On Windows, Novus libraries often use `win_call` instead of `syscall`.

```novus
win_call("ExitProcess", 0);
```

This pattern appears in platform-specific code such as terminal or environment helpers.

## Conditional compilation matters

Inline assembly is usually wrapped in `#if` blocks:

```novus
#if(os == "darwin") {
    mov(x16, 0x2000000 + 4);
    syscall();
}

#if(os == "windows") {
    win_call("ExitProcess", 0);
}
```

That is the normal way to keep one public API while swapping implementations per OS or architecture.

## When to reach for inline assembly

Use it when you are:

- building a library backend
- wrapping a platform syscall directly
- exposing a missing low-level primitive

Do **not** use it for everyday string handling, arrays, printing, file IO, or process launching if an official library already does that work.

## Best place to learn from real code

Study these sources:

- official Novus docs and legacy docs
- `novus-window`
- `novus-env`
- `novus-process`
- `examples/lib/term/main.nov` in the Novus repo

