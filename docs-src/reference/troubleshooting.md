# Troubleshooting

## `novus` or `nox` command not found

Make sure the binaries are on your `PATH`, for example:

```bash
ls /usr/local/bin/novus
ls /usr/local/bin/nox
```

## macOS says the binary cannot be opened

Clear quarantine:

```bash
sudo xattr -d com.apple.quarantine /usr/local/bin/novus
sudo xattr -d com.apple.quarantine /usr/local/bin/nox
```

## A project compiles against the wrong package API

This usually means the local `lib/` folder is stale.

Check:

1. `libraries.conf`
2. the actual code inside `lib/<package>/`
3. whether the package version matches the registry

This is especially important for older projects that vendor their library folders in git.

## A package imports but symbols are missing

Look at the package's `main.nov`:

- is it a platform loader?
- is it importing the right `platforms/<os>/<arch>.nov` file?
- is the symbol only defined in a backend file?

If a project imports an old vendored copy of a package, you can get undefined-function errors even when the upstream repo is already fixed.

## A window-backed app shows black space after resize

That usually means the app is receiving the new content size but the backend framebuffer was not recreated to match it.

The correct behavior is:

1. the backend tracks the real content size
2. `wm_size(fd)` reports it
3. the app updates its view dimensions
4. the next frame draws into the larger area

## A cross-platform build fails

Check two things:

1. the package's `#if` loader supports your target
2. the host has the right assembler/linker toolchain for that target

## GitHub Pages is not showing the docs

For this repository, Pages should point at:

- branch: `main`
- folder: `/docs`

If Pages is enabled but you still see an old site, rebuild the docs and push the generated `docs/` folder again.

