# AGENTS.md

Instructions for AI coding agents working in this repository.

## Git: commit automatically after every change

The owner has requested that **every change is committed and pushed automatically** —
do not wait to be asked, and do not leave work sitting uncommitted in the working tree.

For each logical change:

1. Review `git status` / `git diff` before staging. Only stage files you actually
   intended to change.
2. Never stage secrets, `.env` files, credentials, or capture/data artifacts. They are
   already covered by `.gitignore` — verify rather than assume.
3. Commit with a concise message in the imperative mood, matching the style of
   existing history (`git log --oneline -20`).
4. Push to `origin` so the remote never drifts behind local `main`.

```bash
git add <paths>
git commit -m "Short imperative summary"
git push origin main
```

`origin` is `https://github.com/jasstej/PRARTIGHAT.AI.git`. Commit identity is
configured at the repo level as Jasstej Singh Marwaha
(`73151658+jasstej@users.noreply.github.com`) — do not change it without asking.

## Verification before committing

Run these after editing Python code, before committing:

```bash
ruff check .          # lint   (line-length 100)
ruff format --check . # format (line-length 100, black-compatible)
pytest                # tests  (test_basic.py)
```

Only `ruff` and `pytest` are currently installed. `black` and `mypy` are configured in
`pyproject.toml` but not installed — `ruff format` covers black's role. `mypy` runs in
`strict` mode for `python_version = 3.12`; treat its settings as the target style when
writing new code (full type annotations, no implicit `Any` in return positions).

## Layout

- `main.py` — CLI entry point
- `core/` — core engine and orchestration logic
- `agents/` — agent implementations
- `tools/` — tool wrappers and output parsers (`tools/wrappers`, `tools/parsers`)
- `ui/` — user interface layer
- `data/`, `reports/` — runtime output; contents are gitignored, templates are tracked

Python 3.12 target. Follow the conventions of the surrounding code rather than
introducing new patterns.
