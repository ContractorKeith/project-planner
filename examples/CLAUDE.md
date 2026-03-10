# TaskTrail

## What this is
A CLI task tracker for developers who live in the terminal. Fast capture, fast
retrieval, local storage — no server, no account.

## User
Solo developers and terminal-power-users who want task management without
leaving the command line.

## Stack
- **Language:** Python 3.11+
- **Architecture:** Single CLI tool
- **Data:** SQLite (`~/.tasktrail/tasks.db`)
- **Key deps:** click, rich, sqlite3 (built-in)
- **Deploy:** Local install via pip/pipx

## Structure
[Fill in once repo is scaffolded]

## Conventions
[Fill in as conventions emerge]

## Do NOT
- Build a GUI or web interface
- Add cloud sync or multi-device support
- Add team/collaboration features
- Add calendar or due-date reminders
- Use SQLAlchemy — direct sqlite3 is sufficient

## Current State
Planning complete. Ready to build. See PRD.md and TASKS.md for details.

## Success Criteria
1. Add a task in under 2 seconds with a single command
2. List all open tasks, filtered by tag or priority
3. Mark tasks complete and view a done log
4. Data persists between sessions in a local SQLite file
5. Works on macOS and Linux without extra dependencies
