# dct-docs

MkDocs site for Bluecom eSIM platform partner documentation, deployed to GitHub Pages.

## Local preview

Requires [uv](https://docs.astral.sh/uv/).

```bash
uv sync
uv run mkdocs serve
```

Open http://127.0.0.1:8000.

## Manage dependencies

```bash
uv add <package>          # add
uv remove <package>       # remove
uv lock --upgrade         # bump lockfile
```

## Adding docs

1. Drop the `.md` file under `docs/`.
2. Add it to the `nav:` section in `mkdocs.yml`.
3. Commit to `main` — the `Deploy MkDocs to GitHub Pages` workflow publishes automatically.

## GitHub Pages setup

In the repo settings → Pages → Source: **GitHub Actions**.
