# TaskTrail — Stack Decisions

**Date:** 2025-06-15

---

## Architecture

**Pattern:** Single CLI tool
**Rationale:** This is a personal productivity tool with no UI and no server.
A single-entry-point CLI with local storage is the simplest shape that fits.

## Runtime & Language

Python 3.11+

## Key Dependencies

| Package | Purpose |
|---|---|
| click | CLI framework — cleaner than argparse, supports groups and help generation |
| sqlite3 | Built-in — no install needed, handles all persistence |
| rich | Terminal output formatting — tables, colors, progress indicators |

## Data Layer

SQLite — single file at `~/.tasktrail/tasks.db`. Chosen over flat files for
query flexibility (filter by tag, priority, status) without writing a parser.

## Agents & MCPs

None — this project does not use AI agents.

## Deployment

Local install via `pip install .` or `pipx`. No server, no container.

## What We're NOT Using

- **PostgreSQL** — overkill for a single-user local tool
- **Typer** — Click is more mature and has broader community support
- **SQLAlchemy** — direct sqlite3 is sufficient for 3-4 simple tables
- **Docker** — no deployment target, runs directly on the host
