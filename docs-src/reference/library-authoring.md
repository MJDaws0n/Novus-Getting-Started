# Authoring libraries

If you want to build a package for Nox, design it so downstream projects can import it cleanly and update it safely.

## Recommended structure

```text
my-library/
├── main.nov
├── VERSION
├── libraries.conf
├── docs.md
├── tests/
└── platforms/
    ├── darwin/
    ├── linux/
    └── windows/
```

## `main.nov` should be the public loader

That file should expose the library's public surface and select the right backend if needed:

```novus
module my_library;

#if(os == "darwin") {
    import platforms/darwin/arm64;
}

#if(os == "linux") {
    import platforms/linux/common;
}
```

The goal is simple:

- user code imports one stable entrypoint
- the library handles platform selection internally

## `libraries.conf`

Keep the dependency manifest accurate. If your package depends on `std`, `net`, `env`, or anything else, declare it so Nox can resolve dependencies when users install your library.

## `VERSION`

Include a plain version file so registry updates and release automation can read the current version directly.

## `docs.md`

Every package should document:

- what the library is for
- how to import it
- the public functions
- platform support
- any required helper binaries or external tools

## Tests

Official low-level libraries should include tests for every supported OS and architecture, especially where inline assembly or platform syscalls are involved.

## Publishing flow

At a high level:

1. finish the code and tests
2. bump `VERSION`
3. push the repo
4. create a PR against the Nox registry repo to update the package entry

## Keep the public API small

The best Novus libraries expose a tight public surface and hide platform-specific chaos behind it. `window`, `env`, `process`, and `file_io` are all better to use when the platform split lives inside the package rather than inside every application.
