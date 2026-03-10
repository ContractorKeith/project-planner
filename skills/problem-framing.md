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

You need four things. Don't move on until all four are clear:

1. **The problem** — What is broken, missing, or painful right now?
2. **Who has it** — Who is the user? (Could be "just me", that's fine.)
3. **Success criteria** — How will you know when it's solved?
4. **Out of scope** — What is this explicitly NOT? This one is non-negotiable.

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

**Step 4 — Define success**
> "How would you know this is working? What does 'done' look like for you?"

Push for something concrete. "It saves me time" is not a success criterion.
"I can process a quote in under 5 minutes instead of 30" is.

**Step 5 — Lock out of scope**
This is the most important and most skipped question:
> "What is this specifically NOT trying to do? What should we leave out?"

If they struggle to answer, prompt: "What's something a well-meaning developer might
add that you'd actually want removed?"

---

## When the problem is locked

Summarize back to the user in 3-5 sentences:
- The problem in one sentence
- Who has it
- What success looks like
- What's out of scope

Then ask: **"Does that capture it accurately?"**

Do not proceed to stack-selection until you get a yes.

---

## What to capture (for prd-writing skill later)

Store these answers in the session. The prd-writing skill will pull from them.

```
PROBLEM_STATEMENT: [one sentence]
USER: [who]
SUCCESS_CRITERIA: [concrete, measurable if possible]
OUT_OF_SCOPE: [explicit list]
CONTEXT: [anything else relevant — existing tools, constraints, backstory]
```

---

## Common failure modes to avoid

- **Solution drift** — User keeps describing features. Keep redirecting to the problem.
- **Vague success** — "Better UX" is not a success criterion. Push for specifics.
- **Missing out-of-scope** — If you skip this, the PRD will be ambiguous. Don't skip it.
- **Assuming the user** — "Customers" and "just me" require completely different solutions.
