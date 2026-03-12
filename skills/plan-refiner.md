---
name: plan-refiner
description: Refine an existing project plan after a sprint or iteration. Use this skill when the user already has files in /outputs/ and wishes to "refine an existing plan", "plan sprint 2", or "resolve open questions" rather than starting from a completely blank slate.
---

# Plan Refiner

## Purpose
When a user returns to the `project-planner` repository after successfully building their first iteration (or just completing Sprint 1), they want to update their existing documents rather than rewrite their PRD and Stack decisions from scratch. This skill allows the AI to act as a partner in scoping out the next phase of work.

---

## Prerequisites
- Files must already exist in `/outputs/` (e.g. `PRD.md`, `STACK.md`, `TASKS.md`).
- You must read these files to understand the current state of the project before prompting the user.

---

## What you are extracting

Instead of framing the problem from scratch, you need to understand what has changed and what they want to tackle next:

1. **Sprint Review** — What was completed? Did everything in Sprint 1 work as expected?
2. **Current Pain/Goal** — Why are they back? What is the core goal for this exact refinement session?
3. **Open Questions** — Are there any open questions in the current `PRD.md` that can now be answered?

---

## How to run this

Ask one question at a time. Do not present a form.

### Step 1 — Review and acknowledge
Before asking anything, read the `/outputs/` folder. Acknowledge what was in the last plan.
> "I see we have a plan for [Project Name]. Are we planning Sprint 2, or did something change about the overall direction?"

### Step 2 — Clarify current goals 
> "What is the most important feature or goal for this next iteration?"

Ensure they don't list 20 features. Keep them focused.

### Step 3 — Scope out the next sprint (Sprint 2)
> "To reach that goal, what are the smallest logical chunks of work we need to build?"

### Step 4 — Resolve Open Questions
If the existing `PRD.md` has open questions, ask the user if they want to resolve any of them now, one at a time. If they do not, leave them as open questions.

---

## What to update (for prd-writing skill)

Once you've scoped the new iteration, you will need to update the existing files in `/outputs/`. 
Do *not* run the full `prd-writing.md` process. Instead, just edit the existing files:

1. **`PRD.md`**: Update Status/Date, move completed items to "Done", and update the "In Scope" / "Open Questions" sections.
2. **`STACK.md`**: Do not change unless they explicitly mentioned introducing a new tech dependency.
3. **`TASKS.md`**: Move the completed "Sprint 1" tasks under "Done". Take the newly agreed upon tasks and format them as the new "Sprint 2" section. 
4. **Context File (`CLAUDE.md`, `GEMINI.md`, etc)**: Update the "Current State" to reflect that this is Sprint 2 or Iteration 2 setup.

---

## When the refinement is complete

Say:
> "I've refined your `/outputs/` documents with the new goals. You can drop this updated folder into your repo to start the next iteration."
