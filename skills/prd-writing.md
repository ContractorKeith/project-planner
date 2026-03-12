---
name: prd-writing
description: Synthesize a completed planning session into the /outputs/ handoff package. Use this skill after both problem-framing and stack-selection are confirmed. Produces PRD.md, STACK.md, TASKS.md, and a context file — everything needed to start building in the next repo.
---

# PRD Writing

## Purpose
Take everything captured during the planning session and produce a clean, complete
handoff package in `/outputs/`. This is the last step in every planning session.
The user should be able to hand this folder to any AI coding assistant — or another
developer — and have them immediately understand what to build and why.

---

## Prerequisites
- Problem framing confirmed by user
- Stack selection confirmed by user
- All four problem fields captured: PROBLEM_STATEMENT, USER, SUCCESS_CRITERIA, OUT_OF_SCOPE
- All stack fields captured: ARCHITECTURE, LANGUAGE, DEPENDENCIES, DATA_LAYER, DEPLOYMENT

---

## Output files to generate

Generate all four files. Use the structures below to generate each file.

---

### 1. PRD.md — The primary artifact

This is the document a developer (or AI) reads to understand what they're building.
Keep it tight. No fluff. Every section earns its place.

```markdown
# [Project Name] — Product Requirements Document

**Status:** Draft  
**Date:** [today]  
**Author:** [user name if known, otherwise omit]

---

## Problem

[PROBLEM_STATEMENT — one clear sentence]

[1-2 sentences of context: why this matters, what happens without it]

## User

[USER — who this is for and what they care about]

## Solution

[2-3 sentences describing the solution at a high level. Not features. The approach.]

## Success Criteria

[Numbered list. Concrete. Measurable where possible.]

1. [criterion]
2. [criterion]

## Scope

### In Scope
[Bulleted list of what this project does]

### Out of Scope
[Bulleted list of what it explicitly does not do]

## Key Decisions

[Any important decisions made during planning that affect the build]

## Open Questions

[Anything unresolved that the builder will need to answer. Can be empty.]
```

---

### 2. STACK.md — Technical decisions

```markdown
# [Project Name] — Stack Decisions

**Date:** [today]

---

## Architecture

**Pattern:** [pattern name]  
**Rationale:** [why this pattern fits the problem]

## Runtime & Language

[language + version]

## Key Dependencies

| Package | Purpose |
|---|---|
| [name] | [why] |

## Data Layer

[SQLite / Postgres / flat files / none — and why]

## Agents & MCPs

[List with purpose, or "None — this project does not use AI agents"]

## Deployment

[Where and how it runs]

## What We're NOT Using

[Anything explicitly ruled out, with a brief reason]
```

---

### 3. TASKS.md — First sprint

Keep this realistic. 5-10 tasks max for a first sprint. If you can't ship something
in the first sprint, the tasks are too big.

```markdown
# [Project Name] — Tasks

---

## Sprint 1 — Foundation (Walking Skeleton)

Keep Sprint 1 focused on a "Walking Skeleton" — build an end-to-end connected system with bare-minimum functionality (e.g., UI → API → Database connected and returning "hello world" or mocked data) before adding any real features.

- [ ] [Task: set up repo, initialize project, confirm it runs]
- [ ] [Task: build the walking skeleton (e.g. wire up minimal UI, routing, and database for an end-to-end slice)]
- [ ] [Task: first real feature, smallest useful slice]
- [ ] [Task: ...]

## Backlog

- [ ] [Future feature — not sprint 1]
- [ ] [Future feature — not sprint 1]

## Done

[Empty until you start building]
```

---

### 4. Context file for the next repo

This is the most important output. It drops directly into your build repo
and gives the AI full context immediately.

**File naming:** Name this file based on the tool the user is working with:
- `CLAUDE.md` — Claude Code (default if unsure)
- `AGENTS.md` — OpenAI Codex
- `GEMINI.md` — Gemini CLI

> If the user will use **mvp-builder**, name this file `CONTEXT.md` instead —
> it avoids overwriting mvp-builder's own orchestrator.

```markdown
# [Project Name]

## What this is
[PROBLEM_STATEMENT]. [One sentence on the solution approach.]

## User
[USER]

## Stack
- **Language:** [runtime + version]
- **Architecture:** [pattern]
- **Data:** [data layer]
- **Key deps:** [list]
- **Deploy:** [target]

## Structure
[Fill in once repo is scaffolded — leave as placeholder for now]

## Conventions
[Fill in as conventions emerge — leave as placeholder for now]

## Do NOT
[Anything explicitly out of scope from the PRD]

## Current State
Planning complete. Ready to build. See PRD.md and TASKS.md for details.

## Success Criteria
[Copy from PRD]
```

---

## After generating outputs

1. Tell the user all four files are in `/outputs/`.
2. Update Session State in `skills/orchestrator.md`:
   - Problem locked: yes
   - Stack locked: yes
   - Outputs generated: yes
   - Project name: [name]
3. Say: **"Your planning docs are in `/outputs/`. Drop that folder into your next repo and you're ready to build."**

---

## Quality check before handing off

Before calling it done, verify:
- [ ] PRD has no open questions that would block building
- [ ] STACK.md has actual decisions, not option lists
- [ ] TASKS.md sprint 1 is shippable in a reasonable session
- [ ] Context file gives enough context for a cold-start AI to understand the project
- [ ] Out of scope is explicit in both PRD.md and the context file
