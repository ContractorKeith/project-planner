---
name: multi-model-review
description: Send your completed plan to a second model (or a fresh session) to find gaps, bad assumptions, and missing requirements before handing off to build. Use after outputs/ are generated but before calling planning done.
---

# Multi-Model Review

## Purpose
One model planned this. That same model will struggle to find flaws in its own
reasoning. A second model — or even the same model with no prior context — will
read the plan cold and spot things the planner rationalized away.

This isn't about the plan being bad. It's about not letting the planner grade
its own work.

---

## When to use

After `prd-writing` completes and `/outputs/` has `PRD.md`, `STACK.md`, and `TASKS.md`.
Before handing off to the builder.

If you're unsure whether the plan is solid — run this. If the user says "does
this look right to you?" — run this.

---

## How to do it

### What to send

Bundle these three files into a single prompt. Don't send them separately:

```
Here is a software plan. Your job is to find problems with it — not validate it.

## PRD
[contents of PRD.md]

## STACK
[contents of STACK.md]

## TASKS
[contents of TASKS.md]
```

### What to ask

Add this after the plan:

```
Review this plan from a skeptical perspective:

1. What requirements are unclear, ambiguous, or missing entirely?
2. What assumptions did the planner make that might be wrong?
3. Are there features the user probably expects that aren't in the PRD?
4. Does the task list in TASKS.md cover what the PRD actually requires?
5. What's the most likely way this build fails?

Be direct. List problems, not affirmations.
```

### How to run it

Option A — Different model: Paste the prompt into a different AI than the one
that wrote the plan.

Option B — Fresh session: Start a new conversation with the same model. No prior
context. Paste the prompt cold.

Either works. The goal is no shared reasoning history with the planning session.

---

## What to do with the results

Read the review output. For each issue raised:

- **Missing requirement** — Add it to `PRD.md` with a note that it came from review.
- **Bad assumption** — Surface it to the user. Ask if the assumption holds.
- **Task gap** — Add the missing task to `TASKS.md`.
- **Disagreement between plans** — Don't average them. Pick a side and note why.
  If the models fundamentally disagree on approach, that's a signal to surface to
  the user before building.

Update `/outputs/` with any changes before calling planning done.

---

## When models disagree

If the reviewer flags something the original planner got right — that's fine.
Note the disagreement and move on. One dissent doesn't mean the plan is wrong.

If the reviewer flags something fundamental — scope creep, wrong user assumption,
architecture that won't scale — that's worth stopping for. Don't paper over it.

The rule: surface real disagreements to the user. Don't silently resolve them.

---

## Common failure modes

- **Reviewing with the same context** — If you run the review in the same conversation
  that produced the plan, you'll get rationalization, not review. Fresh context is
  the whole point.
- **Asking for validation instead of critique** — The prompt must ask for problems.
  A neutral prompt gets a neutral (useless) response.
- **Treating every flag as a blocker** — The reviewer will find edge cases and
  nitpicks. Use judgment. Real gaps and wrong assumptions are blockers.
  Missing polish items are not.
- **Skipping this when the plan feels solid** — Plans that feel solid are exactly
  when this matters. Obvious plans have obvious blind spots.
