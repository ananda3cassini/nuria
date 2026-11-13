# Decisions

Lightweight ADRs. Newest decisions are appended at the end.

## 001 Python project managed with uv
- **Date:** 2026-11-07
- **Decision:** Manage the project, virtual environment and dependencies with uv.
- **Why:** A lockfile gives reproducible installs; one tool covers both venv and dependencies.
- **Alternatives considered:** pip + venv (standard but manual, no lockfile by default). Docker was discussed: it isolates a whole system, a different problem, planned for step 5.

## 002 Real medical data only in data/, fake reports in samples/
- **Date:** 2026-11-10
- **Decision:** Real reports stay in `data/` (git-ignored). Tests and demos use fictitious reports in `samples/`.
- **Why:** The repo is public and under the owner's name, so redacting real reports would not anonymise them. Git history is permanent. Redacted real reports stay in `data/` for real use.
- **Alternatives considered:** Commit redacted real reports.

## 003 Protect data/ and .env with permission deny rules + OS sandbox
- **Date:** 2026-11-10
- **Decision:** Block Claude Code from `data/` and `.env` with permission deny rules plus the OS sandbox, in strict mode with `failIfUnavailable`.
- **Why:** The OS enforces the sandbox for every program. A hook only sees the commands it parses. Each layer was tested with a fake file.
- **Alternatives considered:** A PreToolUse hook that inspects commands.

## 004 Long context instead of RAG for V1
- **Date:** 2026-11-07
- **Decision:** V1 sends the summary sheets, measurements and active prescriptions directly in the prompt.
- **Why:** About 8 reports fit in the context. Each PDF is sent once; the chat reads sheets and measurements. Prompt caching keeps repeated context cheap. Revisit after the V1 evaluation.
- **Alternatives considered:** RAG (embeddings + retrieval).

## 005 Modular monolith
- **Date:** 2026-11-13
- **Decision:** One application, one sub-package per responsibility in `src/nuria/`.
- **Why:** Clear boundaries without the deployment and network overhead of separate services.
- **Alternatives considered:** Microservices.

## 006 Learning log kept private, outside the repository
- **Date:** 2026-11-07
- **Decision:** The learning log is not stored in this repository.
- **Why:** The repository is public; the log is personal.
- **Alternatives considered:** A `docs/` learning log in the repo.
