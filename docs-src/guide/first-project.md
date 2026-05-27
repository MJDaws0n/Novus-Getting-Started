# Your first project

--8<-- "includes/status-warning.md"


This is the quickest clean path into Novus.

## Create a project with Nox

```bash
nox init my-app
cd my-app
```

That gives you a starter project with:

```text
my-app/
├── main.nov
├── libraries.conf
├── lib/
│   └── std/
└── src/
    └── app.nov
```

`nox init` already pulls the standard library, so you can start writing code immediately.

For a tiny app, keeping everything in `main.nov` is fine. Once the project grows, put the real code in `src/` and keep the root `main.nov` as a small loader that imports your app modules and calls into them.

## The starter file

A minimal project usually looks like this:

```novus
module my_app;

import lib/std std;

fn main() -> i32 {
    std.print("Hello, world!");
    std.exit(0);
    return 0;
}
```

### What each line means

- `module my_app;` gives the file a module name.
- `import lib/std std;` imports the `std` package and aliases it to `std`.
- `fn main() -> i32` is the entrypoint.
- `std.exit(0)` exits the process cleanly.

## Compile it

```bash
novus main.nov
```

You should get output in:

```text
build/<target>/
```

For example on macOS arm64:

```text
build/darwin_arm64/main
```

Run it:

```bash
./build/darwin_arm64/main
```

## Add a second function

```novus
module my_app;

import lib/std std;

fn greet(name: str) -> void {
    std.print("Hello " + name);
}

fn main() -> i32 {
    greet("Novus");
    std.exit(0);
    return 0;
}
```

On a larger project, `greet` and the rest of your app code would usually move into `src/`, while `main.nov` stays at the root and just wires the imports together.

## What `libraries.conf` does

Nox keeps your dependencies in `libraries.conf`.

Modern projects often contain lines like:

```conf
installed=std

pkg:std:source=registry
pkg:std:url=https://github.com/MJDaws0n/novus-std
pkg:std:version=1.3.1
```

This file is important because it tells Nox:

- which packages are installed
- where they came from
- which version to use

## Pull another package

```bash
nox pull window
```

That places the package into `lib/window/` and updates `libraries.conf`.

At that point your code can import it:

```novus
import lib/window/main window;
```

## Common beginner mistakes

1. Running `novus` from the wrong directory.
2. Forgetting to run `nox init` first.
3. Editing code while an old `lib/` directory is still checked in from a previous package version.
4. Mixing old and new import styles without checking the package entrypoint.
