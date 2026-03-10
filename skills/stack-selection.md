---
name: stack-selection
description: Define the technical shape of a solution after the problem is locked. Use this skill after problem-framing is complete. Covers tech stack, architecture pattern, agents/MCPs/APIs, deployment, and constraints. Produces decisions with rationale, not a menu of options.
---

# Stack Selection

## Purpose
Translate a locked problem into a concrete technical direction. The output is a
set of decisions — not a list of options — each with a rationale the user can
challenge or accept. By the end, both you and the user know exactly what you're building with.

---

## Prerequisites
- Problem framing is complete and confirmed by the user.
- You know: what it does, who it's for, success criteria, out of scope.

---

## What you're extracting

Work through these four areas in order. Ask one question at a time.

### 1. Constraints
Start here. Constraints eliminate options before you evaluate them.

Questions to work through (pick what's relevant, don't ask all):
- "Are there tools or platforms you already use that this needs to connect with?"
- "Is there anything you're committed to using, or anything you'd rather avoid?"
- "Is this solo or will others work on or use this?"
- "Any timeline pressure, or are we building this right?"
- "Budget constraints — self-hosted vs managed services matter here."

### 2. Scale and complexity
- "Is this a personal tool, an internal tool for a small team, or something bigger?"
- "Rough estimate on data volume — hundreds of records, thousands, millions?"
- "Does it need to run offline, or is always-connected fine?"

### 3. Architecture pattern
Based on what you know, suggest a pattern and explain why. Common patterns for
the kinds of projects this repo plans:

| Pattern | Use when |
|---|---|
| **Single script / CLI** | Solo tool, no UI, output to terminal or file |
| **Local app + SQLite** | Personal tool, needs persistence, no server |
| **API + lightweight frontend** | Small team, browser access needed |
| **Agent + MCP tools** | Automation-heavy, needs to call external services |
| **Pipeline / cron** | Background processing, no user interaction |

Don't present this table to the user. Use it to make a recommendation.

### 4. Agent and MCP considerations
If the project involves AI agents or tool use:
- "Does this need to call external APIs? Which ones?"
- "Is there an existing MCP server for that, or would we need to build one?"
- "Should the AI be in the loop on every action, or just at certain decision points?"

For simple tools — don't introduce agent complexity. Say so explicitly.

---

## How to make recommendations

Don't offer three options and let the user decide on pure preference. That's not helpful.

Do this instead:
> "Based on what you've told me, I'd go with [pattern] using [tech]. Here's why: [1-2 sentences].
> The main tradeoff is [honest tradeoff]. Does that direction make sense?"

If the user pushes back, explore their reasoning. Sometimes they have a constraint
they haven't mentioned yet.

---

## When stack is locked

Summarize the decisions:

```
ARCHITECTURE: [pattern name]
LANGUAGE/RUNTIME: [specific version if known]
KEY DEPENDENCIES: [libraries, frameworks]
DATA LAYER: [SQLite / Postgres / flat files / none / etc.]
AGENTS/MCPS: [list or "none"]
DEPLOYMENT: [local / Cloudflare / VPS / etc.]
OUT OF SCOPE (tech): [what we're not building]
RATIONALE: [2-3 sentences on why this shape fits the problem]
```

Ask: **"Does this match what you had in mind?"**

Don't proceed to prd-writing until you get a yes.

---

## Common failure modes to avoid

- **Gold plating** — Don't suggest Kubernetes for a personal CLI tool.
- **Option paralysis** — Make a recommendation. Explain it. Let them respond.
- **Skipping constraints** — What they already use often determines the answer.
- **Assuming AI is needed** — Many good tools have no AI in them at all.
- **Ignoring the solo dev** — If it's a solo developer, a complex microservice architecture
  is wrong by definition.
