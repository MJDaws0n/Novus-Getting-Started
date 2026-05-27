# Library reference

This section lists the wrapper-style functions exposed by the Novus libraries in the current registry ecosystem.

It is designed to be useful for:

- application authors
- library authors
- AI agents trying to understand package surfaces quickly

## Scope of this reference

This reference intentionally focuses on **public wrapper-style functions**.

That means:

- user-facing functions are listed
- low-level helper wrappers are included where they are part of the exported surface
- repeated overload variants are usually grouped under one family name instead of being expanded line by line
- each page now shows the parameters and return type for the documented functions

## Covered libraries

### Core packages

- [std](libraries/std.md)
- [env](libraries/env.md)
- [file_io](libraries/file-io.md)
- [maths](libraries/maths.md)
- [physics](libraries/physics.md)
- [net](libraries/net.md)
- [process](libraries/process.md)
- [time](libraries/time.md)
- [window](libraries/window.md)

### Network / service packages

- [http](libraries/http.md)
- [smtp](libraries/smtp.md)
- [MySQL-Interact](libraries/mysql-interact.md)

## Notes on accuracy

These pages were written from the local package repos and registry state available in this environment.

If you are working in an older project, always check:

1. the package version in `libraries.conf`
2. the actual source code inside `lib/<package>/`
3. the matching registry entry in `Nox/registry.txt`
