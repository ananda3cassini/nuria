# Architecture

## Purpose
Nuria is a local assistant that turns lab-report PDFs into readable summaries and answers questions across dated results and prescriptions. Personal learning project: the owner must understand every change.

## Modules
Modular monolith: one package `src/nuria/`, one sub-package per module.

| Module | Role |
|---|---|
| `extraction` | Read a lab-report PDF and extract its text and measured values. |
| `summaries` | Produce the readable summary sheet of one lab report. |
| `storage` | Store and query measurements and prescriptions in SQLite. Depends on no other Nuria module. |
| `chat` | Answer questions from summary sheets, measurements and active prescriptions. |
| `api` | Expose Nuria to the web front end (FastAPI). |

## Dependency rule
- `api` may call every module.
- `summaries` owns `data/fiches/`: it writes and reads the summary sheets.
- `chat` reads sheets through `summaries` and measurements through `storage`.
- `storage` depends on no other Nuria module.

Not enforced by a test yet.

## Data flow
```
PDF -> extraction -> summary sheet (data/fiches/)
                  -> measurements (SQLite via storage)
                                   -> chat
```
V1 sends the sheets, measurements and active prescriptions in the prompt (long context). No retrieval.

## Where data lives
- `data/`: real medical data. Local only, git-ignored.
- `samples/`: fictitious lab reports. Public, used for tests and demos.

## Status
Step 1 done: the modules are empty placeholders.
