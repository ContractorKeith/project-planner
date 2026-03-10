---
name: skill-creator
description: Create a new skill file and add it to /skills/. Use this whenever the user or orchestrator identifies a capability gap mid-session — something that would be useful now and in future sessions. Trigger when someone says "we need a skill for X", "can you learn how to do Y", or when a repeated pattern emerges that isn't covered by an existing skill.
---

# Skill Creator

## Purpose
Capture a reusable capability as a skill file in `/skills/` so it's available
for this session and every future planning session. Skills are how this repo
gets smarter over time.

---

## When to create a skill

Create a new skill when:
- The orchestrator or user identifies a task not covered by existing skills
- A useful pattern has emerged in the current session worth preserving
- The user explicitly asks for one

Don't create a skill for something you'll only do once. Skills are for
repeatable, reusable capabilities.

---

## How to create a skill

### Step 1 — Capture intent
Ask (or infer from context):
1. What should this skill enable the AI to do?
2. When should it trigger? (What phrases or situations?)
3. What does a good output look like?

If the session has already produced an example of the capability, use that as
your reference. Don't ask questions you can answer from context.

### Step 2 — Write the skill file

Every skill file follows this structure:

```markdown
---
name: skill-name-kebab-case
description: [What it does + when to trigger. Be specific. Be a little pushy —
             mention the exact contexts where this should activate.]
---

# Skill Title

## Purpose
[One sentence. What problem does this skill solve?]

---

## [Main content]
[Instructions, patterns, examples, decision logic]

---

## Output format
[What should the AI produce when this skill runs?]
```

**Rules for the description field (frontmatter):**
- This is the primary trigger mechanism. If it's vague, the skill won't fire.
- Include both what it does AND when to use it.
- Err toward being explicit. "Use this when the user mentions X, Y, or Z" is good.

**Rules for the body:**
- Keep it under 300 lines for a planning skill
- Use imperative instructions ("Ask the user...", "Produce...", "Do not...")
- Include a "Common failure modes" section if there are easy ways to get it wrong

### Step 3 — Save and confirm

Save the file to `/skills/[name].md`.

Tell the user:
> "Created `skills/[name].md`. It's available for the rest of this session and future ones."

---

## Skill anatomy reference

```
skills/
└── your-skill.md
    ├── YAML frontmatter  (name + description — required)
    └── Markdown body     (instructions — required)
```

For complex skills, you can add a subfolder:
```
skills/
└── your-skill/
    ├── skill.md          (main instructions)
    └── references/       (supporting docs loaded as needed)
```

But for planning skills, a single `.md` file is almost always enough.

---

## Quality check before saving

- [ ] The `description` field is specific enough to trigger correctly
- [ ] The skill has a clear, single purpose
- [ ] Instructions are imperative and unambiguous
- [ ] It doesn't overlap substantially with an existing skill
- [ ] It will be useful in future sessions, not just this one
