# Nuria

Local assistant that turns lab-report PDFs into readable summaries and answers questions across dated results and prescriptions. Personal learning project: the owner must understand every change.

## Commands
- Run: `uv run nuria`
- Add a dependency: `uv add <package>` (never `pip install`)
- Tests: `uv run pytest` (from step 2)

## Layout
- All application code lives in `src/nuria/` (modular monolith: one package, one sub-package per module)
- Fake lab reports for tests and demos: `samples/` (to be created)
- Docs: `docs/ARCHITECTURE.md`, `docs/DECISIONS.md` (to be created)

## Rules
- Never read, open or list `data/` or `.env`: they hold real medical data and secrets.
- Never put real medical data, names or API keys in code, tests, commits or docs. Use files from `samples/` only.
- The API key comes from the `ANTHROPIC_API_KEY` environment variable. Never hardcode it.
- For a significant change: read the existing code first, propose a plan, then implement, test on one or two files from `samples/`, and only then integrate. Small fixes need no plan.
- Reuse existing functions in `src/nuria/` before writing new ones. No duplicated logic.
- No new abstraction (base class, factory, config layer) without a concrete second use.
- Ask before adding a dependency, and explain why it is needed.
- V1 sends all fiches, measurements and active prescriptions directly in the prompt (long context). No retrieval, embeddings or agents unless I ask.
- Explain important choices. Skip the obvious.
- Code, comments, file names and commit messages in English.