# Novus Getting Started

A detailed onboarding repo for **Novus** and **Nox**.

This repository has two jobs:

1. **Human docs** — a polished static site that walks through installation, first projects, inline assembly, `std`, and real project walkthroughs.
2. **AI docs** — a dedicated reference file for agents that need to understand Novus syntax, builtins, imports, packaging, and common ecosystem patterns quickly and accurately.

## Read the docs

- GitHub Pages: <https://mjdaws0n.github.io/Novus-Getting-Started/>
- AI guide: [AI_GUIDE.md](AI_GUIDE.md)
- LLM index: [llms.txt](llms.txt)

## Build the HTML locally

```bash
python3 -m pip install -r requirements-docs.txt
./build-docs.sh
open docs/index.html
```

`mkdocs.yml` uses:

- `docs-src/` for the Markdown source
- `docs/` for the generated HTML output

That means the repo always contains a folder of real static HTML that can be opened locally or published with GitHub Pages.

## Covered topics

- Installing Novus and Nox
- Creating your first project
- Writing Novus code
- Using `std`
- Pulling libraries with Nox
- Inline assembly and low-level builtins
- Building the platformer game
- Building the Todo app
- Library authoring patterns
- AI-oriented language reference

