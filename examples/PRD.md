# TaskTrail — Product Requirements Document

**Status:** Draft
**Date:** 2025-06-15
**Author:** Jane Developer

---

## Problem

Managing personal tasks across sticky notes, text files, and memory leads to
dropped commitments and wasted time looking for what's next.

A lightweight CLI task tracker that lives where developers already work — the
terminal — eliminates the friction of switching to a separate app.

## User

Solo developers and terminal-power-users who want fast task capture and retrieval
without leaving the command line.

## Solution

A Python CLI tool that stores tasks in a local SQLite database. Users add, list,
complete, and filter tasks with short commands. No server, no account, no sync —
just a fast local tool.

## Success Criteria

1. Add a task in under 2 seconds with a single command
2. List all open tasks, filtered by tag or priority
3. Mark tasks complete and view a done log
4. Data persists between sessions in a local SQLite file
5. Works on macOS and Linux without extra dependencies

## Scope

### In Scope
- Add, list, complete, delete tasks via CLI
- Tag and priority support
- SQLite storage in `~/.tasktrail/`
- Basic search/filter
- Shell completion for common commands

### Out of Scope
- GUI or web interface
- Cloud sync or multi-device support
- Team/collaboration features
- Calendar or due-date reminders
- Mobile app

## Key Decisions

- SQLite over flat files for query flexibility and data integrity
- Click over argparse for cleaner CLI ergonomics
- No config file needed — sensible defaults, override with flags

## Open Questions

None — ready to build.
