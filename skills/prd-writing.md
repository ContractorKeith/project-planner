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
- The `.session/state.json` file exists and contains both the `problem` and `stack` objects.

---

## Output files to generate

Generate all four files based on the contents of `.session/state.json`. Use the structures below to generate each file.

---

### 1. PRD.md — The primary artifact

This is the document a developer (or AI) reads to understand what they're building.
Keep it tight. No fluff. Every section earns its place.

```markdown
# [Project Name] — Product Requirements Document

**Status:** Draft  
**Date:** [today]  
**Author:** [state.problem.user_name if present, otherwise omit]

---

## Problem

[state.problem.problem_statement]

[state.problem.context]

## User

[state.problem.user]

## Solution

[2-3 sentences describing the solution at a high level. Not features. The approach.]

## Success Criteria

[Numbered list from state.problem.success_criteria]

## Scope

### In Scope
[Bulleted list of what this project does]

### Out of Scope
[Bulleted list from state.problem.out_of_scope]

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

**Pattern:** [state.stack.architecture]  
**Rationale:** [state.stack.rationale]

## Runtime & Language

[state.stack.language_runtime]

## Key Dependencies

| Package | Purpose |
|---|---|
| [name from state.stack.key_dependencies] | [why] |

## Data Layer

[state.stack.data_layer]

## Agents & MCPs

[state.stack.agents_mcps]

## Deployment

[state.stack.deployment]

## What We're NOT Using

[state.stack.out_of_scope_tech]
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
[state.problem.problem_statement]. [One sentence on the solution approach.]

## User
[state.problem.user]

## Stack
- **Language:** [state.stack.language_runtime]
- **Architecture:** [state.stack.architecture]
- **Data:** [state.stack.data_layer]
- **Key deps:** [state.stack.key_dependencies]
- **Deploy:** [state.stack.deployment]

## Structure
[Fill in once repo is scaffolded — leave as placeholder for now]

## Conventions
[Fill in as conventions emerge — leave as placeholder for now]

## Do NOT
[state.problem.out_of_scope]

## Current State
Planning complete. Ready to build. See PRD.md and TASKS.md for details.

## Success Criteria
[state.problem.success_criteria]
```

---

## After generating outputs

1. Tell the user all four files are in `/outputs/`.
2. Say: **"Your planning docs are in `/outputs/`. Drop that folder into your next repo and you're ready to build."**
3. Delete the `.session/state.json` file to clean up the session.

---

## Quality check before handing off

Before calling it done, verify:
- [ ] PRD has no open questions that would block building
- [ ] STACK.md has actual decisions, not option lists
- [ ] TASKS.md sprint 1 is shippable in a reasonable session
- [ ] Context file gives enough context for a cold-start AI to understand the project
- [ ] Out of scope is explicit in both PRD.md and the context file
