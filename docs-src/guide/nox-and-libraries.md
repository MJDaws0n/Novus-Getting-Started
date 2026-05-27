# Nox and libraries

Nox is what turns Novus from "a compiler you can run once" into a reusable ecosystem.

## Initialise a project

```bash
nox init my-app
```

That creates the project skeleton and pulls `std`.

## Install a registry package

```bash
nox pull window
nox pull file_io
```

Nox downloads packages into `lib/<name>/`.

## What `libraries.conf` is for

This file is the package manifest for the project.

Modern example:

```conf
installed=std,file_io

pkg:std:source=registry
pkg:std:url=https://github.com/MJDaws0n/novus-std
pkg:std:version=1.3.0
```

Older projects may include:

- `branch=...`
- `commit=...`
- version ranges

You will still see those in some repositories.

## Importing installed packages

Once a package is present in `lib/`, import it from code:

```novus
import lib/file_io fio;
import lib/window/main window;
```

## Recommended app layout

For larger applications, keep the repository root simple and move most code into `src/`:

```text
my-app/
├── main.nov
├── libraries.conf
├── lib/
│   └── std/
└── src/
    ├── app.nov
    └── features/
```

The usual pattern is:

- root `main.nov` stays small
- `main.nov` imports files from `src/`
- feature code lives in `src/` subfolders

## Updating projects safely

If a project starts throwing strange errors after a package ecosystem change, check:

1. the `libraries.conf` version
2. the actual code inside `lib/<package>/`
3. whether the project has a stale vendored package copy

That specific problem appears often when older projects keep package directories checked into git.

## Library layout

Application layout and library layout are slightly different.

For libraries, keep using the dedicated guidance in [Authoring libraries](../reference/library-authoring.md). That page covers the public `main.nov` loader, `VERSION`, `docs.md`, tests, and platform folders.
