---
name: phase-gates
description: Run a structured checklist before considering /outputs/ complete. Catches half-baked plans before they reach the builder. Use at the end of every planning session, after prd-writing finishes but before you tell the user planning is done.
---

# Phase Gates

## Purpose
A plan that feels done often isn't. Requirements are vague. "Done" is undefined.
Open questions were left open. This skill runs a final checklist before handing
off to the builder — because fixing a bad plan costs minutes; fixing a bad build
costs hours.

---

## When to use

After `prd-writing` completes and before you tell the user the plan is ready.
This is the last step of every planning session. Not optional.

---

## The checklist

Run through these in order. A "no" on any item means the plan isn't done yet.

### Problem definition
- [ ] Is the problem stated in one clear sentence?
- [ ] Is the user (or users) explicitly named?
- [ ] Is out-of-scope stated explicitly, not implied?

### Scope
- [ ] Does every feature in TASKS.md trace back to a requirement in the PRD?
- [ ] Are there any features that crept in during planning that the user didn't ask for?
- [ ] Is the scope achievable in a first build, or does it need to be phased?

### Done criteria
- [ ] For every feature in the PRD, is "done" defined concretely?
  ("User can log in" is not done criteria. "User submits credentials, session
  is created, they see the dashboard" is.)
- [ ] Are there success criteria that are actually verifiable?

### Open questions
- [ ] Are there any questions from the planning session that were never resolved?
- [ ] Are there any "TBD" or "we'll figure this out later" notes in the PRD?
- [ ] Are there integration points or dependencies that are still unknown?

### Assumptions
- [ ] Are assumptions documented explicitly in the PRD?
- [ ] Has the user confirmed the most critical assumptions?

---

## What to do when items fail

**One or two unchecked items** — Fix them inline before presenting to the user.
Most gaps can be resolved in a sentence or two.

**Three or more unchecked items** — Something is wrong with the plan structure,
not just the details. Go back to the relevant skill (`problem-framing`,
`stack-selection`, or `prd-writing`) and work through it properly.

**Open questions that require a user decision** — Surface them clearly:

> "Before we call the plan done, I need a few answers:
> 1. [specific question]
> 2. [specific question]
> Once you answer these, I'll update the PRD and we're ready."

Don't hand off a plan with unresolved user questions. The builder will make up
answers, and those answers will be wrong.

---

## How to present the result

If the checklist passes, say:

> "Phase gate passed. `/outputs/` is ready to hand off to the builder."

If items were resolved during the check, note what changed:

> "Phase gate passed — I clarified the done criteria for [feature] and documented
> the assumption about [X]. Outputs are updated and ready."

If the user needs to make a decision, wait for the answer before passing the gate.

---

## Common failure modes

- **Running this as a formality** — If you check boxes without actually reading the
  PRD, you'll miss real gaps. Treat each item as a genuine question.
- **Passing with known open questions** — "The user can figure that out during build"
  is not a plan. The builder will make something up. Surface it now.
- **Missing "done" criteria** — This is the most common gap. Vague features produce
  vague implementations. Push for specifics.
- **Skipping the out-of-scope check** — If out-of-scope isn't explicit, the builder
  will fill the gap with something. It will probably be wrong.
