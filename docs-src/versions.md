# Compatibility snapshot

This site is meant to be practical, so here is the ecosystem snapshot it was written against.

| Component | Reference |
| --- | --- |
| Novus compiler | `Novus Compiler V0.2.0` |
| Novus repo | `753ee3c` |
| Nox repo | `632c8be` |
| window library | `1.1.1` |
| Example app: Todo-App | current GitHub repo state on 2026-05-25 |
| Example app: platformer-game | current GitHub repo state on 2026-05-25 |

## Why this matters

Novus and its package ecosystem are still evolving. That means older projects can differ in:

- import style
- `libraries.conf` format
- package layout
- whether a library uses flat files or `platforms/<os>/<arch>.nov`

If something in your local project differs from the examples here, check whether:

1. your `lib/` directory is stale
2. the project was created before the current Nox layout
3. you are reading an older package version

The troubleshooting page covers the most common mismatch patterns.
