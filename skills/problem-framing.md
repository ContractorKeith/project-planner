---
name: problem-framing
description: Extract a clear, locked problem definition from the user before any solution thinking begins. Use this skill at the start of every planning session, immediately after the user describes what they want to build. Keep using it until problem, user, success criteria, and out-of-scope are all defined.
---

# Problem Framing

## Purpose
Lock in the problem before touching the solution. Most projects fail because the
problem was never clearly defined. This skill extracts exactly what you need to
write a PRD that won't drift.

---

## What you're extracting

You need six things. Don't move on until all six are clear:

1. **The problem** — What is broken, missing, or painful right now?
2. **Who has it** — Who is the user? (Could be "just me", that's fine.)
3. **Core workflow** — What are the 2-3 main steps the user takes to go from problem to solution?
4. **Success criteria** — How will you know when it's solved?
5. **Out of scope** — What is this explicitly NOT? This one is non-negotiable.
6. **Your name (optional)** — For the author field in the PRD.

---

## How to run this

Ask one question at a time. Start with the broadest question and narrow from there.
Never present a checklist or a form. The session should feel like a conversation.

### Sequence

**Step 1 — Open question (already asked by orchestrator)**
> "What are you trying to build or solve?"

Let them answer fully. Don't interrupt. Extract everything you can from their first answer.

**Step 2 — Clarify the problem**
If their answer is solution-first ("I want to build an app that..."), redirect:
> "Before we get to the solution — what's the pain or gap that's making you want to build this?"

**Step 3 — Define the user**
> "Who is this for? Just you, your team, customers, or someone else?"

If they say "just me" — great. That's a valid and important answer. Solo tools have
different constraints than multi-user products.

**Step 4 — Define the core workflow**
> "What are the 2-3 main steps the user takes to go from problem to solution in this app?"

This helps visualize the journey rather than just listing features.

**Step 5 — Define success**
> "How would you know this is working? What does 'done' look like for you?"

Push for something concrete. "It saves me time" is not a success criterion.
"I can process a quote in under 5 minutes instead of 30" is.

**Step 6 — Lock out of scope**
This is the most important and most skipped question:
> "What is this specifically NOT trying to do? What should we leave out?"

If they struggle to answer, prompt: "What's something a well-meaning developer might
add that you'd actually want removed?"

**Step 7 — Get user's name (optional)**
> "What is your name? (This will be used in the author field of the PRD. You can skip this if you'd like.)"

---

## When the problem is locked

Summarize back to the user in 3-5 sentences:
- The problem in one sentence
- Who has it
- The 2-3 step core workflow
- What success looks like
- What's out of scope

Then ask: **"Does that capture it accurately?"**

Do not proceed to stack-selection until you get a yes.

---

## What to capture (for prd-writing skill later)

As you collect the answers to these questions, save them to `.session/state.json`.
The `prd-writing` skill will pull from this file.

The JSON object should have a `problem` key with the following structure:

```json
{
  "problem": {
    "problem_statement": "[one sentence]",
    "user": "[who]",
    "core_workflow": "[2-3 main steps]",
    "success_criteria": "[concrete, measurable if possible]",
    "out_of_scope": "[explicit list]",
    "context": "[anything else relevant — existing tools, constraints, backstory]",
    "user_name": "[user's name, or null]"
  }
}
```

---

## Common failure modes to avoid

- **Solution drift** — User keeps describing features. Keep redirecting to the problem.
- **Vague success** — "Better UX" is not a success criterion. Push for specifics.
- **Missing out-of-scope** — If you skip this, the PRD will be ambiguous. Don't skip it.
- **Assuming the user** — "Customers" and "just me" require completely different solutions.
