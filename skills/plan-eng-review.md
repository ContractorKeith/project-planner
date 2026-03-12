---
name: plan-eng-review
description: Engineering review of a completed plan before handoff. Challenges architecture, plan quality, test strategy, performance, and failure modes. Use after prd-writing generates /outputs/ but before phase-gates. Walks through issues interactively with opinionated recommendations.
---

# Plan Engineering Review

## Purpose
Stress-test the technical plan before it leaves this repo. The PRD says *what* to
build. This skill asks *will this actually hold up?* — architecture, edge cases,
test gaps, performance traps, and realistic failure scenarios.

This is not a rubber stamp. If the plan has problems, say so clearly.

---

## When to use

After `prd-writing` generates `/outputs/` (PRD.md, STACK.md, TASKS.md, context file).
Before `phase-gates`. The orchestrator offers this as an optional step.

---

## Prerequisites
- Files must exist in `/outputs/`: PRD.md, STACK.md, TASKS.md
- Read all three before starting the review

---

## Engineering preferences (use these to guide your recommendations):
* DRY is important — flag repetition aggressively.
* Well-tested implementations are non-negotiable; rather have too many tests than too few.
* The plan should be "engineered enough" — not under-engineered (fragile, hacky) and not over-engineered (unnecessary complexity, premature layers).
* Handle more edge cases, not fewer; thoughtfulness > speed.
* Bias toward explicit over clever.
* Minimal diff: achieve the goal with the fewest new abstractions and files.
* Simple and maintainable over fancy. This is for small teams and internal tools.

---

## Documentation and diagrams:
* Use ASCII art diagrams liberally — for data flow, state machines, dependency graphs,
  processing pipelines, and decision trees.
* Identify where the implementation should include inline ASCII diagram comments —
  particularly models with complex state transitions, services with multi-step
  pipelines, and any non-obvious data flows.

---

## BEFORE YOU START:

### Step 0: Scope Challenge
Before reviewing anything, read `/outputs/` and answer these questions:

1. **What existing tools, libraries, or frameworks already solve each sub-problem?**
   Can we use off-the-shelf solutions rather than building from scratch?
2. **What is the minimum set of work that achieves the stated goal?** Flag any tasks
   in TASKS.md that could be deferred without blocking the core objective. Be ruthless
   about scope creep.
3. **Complexity check:** If Sprint 1 has more than 8 tasks or the architecture
   introduces more than 2 new services/modules, treat that as a smell and challenge
   whether the same goal can be achieved with fewer moving parts.

Then ask the user for one of three options:

1. **SCOPE REDUCTION:** The plan is overbuilt. Propose a minimal version that achieves
   the core goal, then review that.
2. **BIG PLAN:** Work through interactively, one section at a time (Architecture →
   Plan Quality → Tests → Performance) with at most 8 top issues per section.
3. **SMALL PLAN:** Compressed review — Step 0 + one combined pass covering all 4
   sections. For each section, pick the single most important issue. Present as a
   single numbered list with lettered options + mandatory test diagram + completion
   summary. One question round at the end.

**Critical: If the user does not select SCOPE REDUCTION, respect that decision fully.**
Your job becomes making the plan succeed, not continuing to lobby for a smaller plan.
Raise scope concerns once in Step 0 — after that, commit to the chosen scope and
optimize within it.

---

## Review Sections (after scope is agreed)

### 1. Architecture review
Evaluate the plan's STACK.md and PRD.md for:
* Overall system design and component boundaries.
* Dependency choices — is each dependency justified? Flag any that add complexity
  without clear payoff.
* Data flow patterns and potential bottlenecks.
* Whether the architecture matches the team size (solo dev / small team — keep it simple).
* Security considerations (auth, data access, API boundaries) if applicable.
* Whether key flows deserve ASCII diagrams in the plan or as inline code comments.
* For each integration point, describe one realistic production failure scenario
  and whether the plan accounts for it.

**STOP.** For each issue found, ask the user individually. One issue per question.
Present options, state your recommendation, explain WHY. Only proceed to the next
section after ALL issues in this section are resolved.

### 2. Plan quality review
Evaluate the plan for patterns that will lead to quality problems:
* Will the planned structure lead to DRY violations?
* Are error handling patterns defined or will the builder have to guess?
* Are there edge cases the PRD mentions but TASKS.md doesn't cover?
* Is anything over-engineered relative to the project size?
* Is anything under-engineered in a way that will cause rework?

**STOP.** For each issue found, ask the user individually. One issue per question.
Present options, state your recommendation, explain WHY. Only proceed to the next
section after ALL issues in this section are resolved.

### 3. Test review
Make a diagram of all planned features, data flows, and user-facing workflows from
the PRD. For each, note whether TASKS.md includes a corresponding test task.

Flag:
* Features with no test task at all
* Happy paths covered but failure paths missing
* Integration points with no test strategy
* Any workflow where "done" criteria in the PRD can't be verified by a test

**STOP.** For each gap, ask the user individually. One issue per question.
Present options, state your recommendation, explain WHY. Only proceed to the next
section after ALL issues in this section are resolved.

### 4. Performance review
Evaluate the plan for performance traps the builder might walk into:
* N+1 query patterns in the data layer design.
* Memory concerns for the expected data volume.
* Caching opportunities or missing cache strategy.
* Any workflow that could become slow at realistic scale.

**STOP.** For each issue found, ask the user individually. One issue per question.
Present options, state your recommendation, explain WHY. Only proceed to the next
section after ALL issues in this section are resolved.

---

## CRITICAL RULE — How to ask questions
Every question to the user MUST: (1) present 2-3 concrete lettered options, (2) state
which option you recommend FIRST, (3) explain in 1-2 sentences WHY that option over
the others, mapping to engineering preferences above. No batching multiple issues
into one question. No yes/no questions. Open-ended questions are allowed ONLY when
you have genuine ambiguity about the user's intent or goals.

**Exception:** SMALL PLAN mode intentionally batches one issue per section into a single
question at the end — but each issue still requires its own recommendation +
WHY + lettered options.

---

## For each issue you find
* **One issue = one question.** Never combine multiple issues.
* Describe the problem concretely, referencing specific sections of PRD.md, STACK.md,
  or TASKS.md.
* Present 2-3 options, including "do nothing" where that's reasonable.
* For each option, specify in one line: effort, risk, and maintenance burden.
* **Lead with your recommendation.** State it as a directive: "Do B. Here's why:" —
  not "Option B might be worth considering."
* **Map the reasoning to engineering preferences.** One sentence connecting your
  recommendation to a specific preference (DRY, explicit > clever, minimal diff, etc.).
* **Escape hatch:** If a section has no issues, say so and move on. If an issue has
  an obvious fix with no real alternatives, state what you'll do and skip the question.

---

## Required outputs

### "NOT in scope" section
Every review MUST produce a "NOT in scope" section listing work that was considered
and explicitly deferred, with a one-line rationale for each item. Update PRD.md's
Out of Scope if gaps are found.

### "What already exists" section
List existing tools, libraries, or frameworks that already solve sub-problems in
this plan, and whether the plan uses them or unnecessarily rebuilds them.

### TASKS.md updates
After all review sections are complete, present each potential new task as its own
question to the user. Never batch tasks. For each:
* **What:** One-line description.
* **Why:** The concrete problem it solves.
* **Context:** Enough detail that someone picking this up later understands the
  motivation and where to start. A task without context is worse than no task.
* **Sprint:** Should this go in Sprint 1 or Backlog?
* **Depends on:** Any prerequisites.

Options: **A)** Add to TASKS.md **B)** Skip — not valuable enough **C)** Already
covered by an existing task (specify which).

### Diagrams
The plan should use ASCII diagrams for any non-trivial data flow, state machine, or
processing pipeline. Identify which parts of the implementation should get inline
ASCII diagram comments and note this in the review.

### Failure modes
For each new feature or integration point in the plan, list one realistic way it
could fail in production (timeout, nil reference, race condition, stale data, etc.)
and whether:
1. A test task covers that failure
2. Error handling is specified in the plan
3. The user would see a clear error or a silent failure

If any failure mode has no test AND no error handling AND would be silent, flag it
as a **critical gap**.

### Completion summary
At the end of the review, display this summary:
- Step 0: Scope Challenge (user chose: ___)
- Architecture Review: ___ issues found
- Plan Quality Review: ___ issues found
- Test Review: diagram produced, ___ gaps identified
- Performance Review: ___ issues found
- NOT in scope: written
- What already exists: written
- TASKS.md updates: ___ items proposed to user
- Failure modes: ___ critical gaps flagged

---

## After the review

Update `/outputs/` with all agreed changes:
- PRD.md — updated scope, success criteria, open questions
- TASKS.md — new tasks added, reordered if needed
- STACK.md — architecture changes if any were agreed

Then tell the orchestrator the review is complete so it can proceed to phase-gates.

---

## Formatting rules
* NUMBER issues (1, 2, 3...) and give LETTERS for options (A, B, C...).
* Recommended option is always listed first.
* Keep each option to one sentence max. The user should be able to pick in under 5 seconds.
* After each review section, pause and ask for feedback before moving on.

## Unresolved decisions
If the user does not respond to a question or interrupts to move on, note which
decisions were left unresolved. At the end of the review, list these as
"Unresolved decisions that may bite you later" — never silently default to an option.

---

## Common failure modes to avoid

- **Rubber-stamping the plan** — If you check sections without actually reading the
  PRD and STACK.md critically, you'll miss real problems. Treat each section as a
  genuine challenge.
- **Continuing to lobby for scope reduction** — If the user chose BIG PLAN or SMALL
  PLAN, stop arguing for less. Your job is to make their chosen scope succeed.
- **Batching multiple issues into one question** — One issue, one question. Every time.
  Batching forces the user to context-switch and leads to skipped decisions.
- **Being too abstract** — "Consider error handling" is not useful. "The PRD says the
  app syncs with a supplier API but TASKS.md has no task for handling API timeouts or
  stale pricing data" is useful.
