---
name: doc-triage
description: Decide which project documents actually need to exist (PRD, TRD, AFD, DBD, BSD, IPD, spec, design brief, schema doc, implementation plan). Use when the user proposes a documentation suite, asks "do we need X doc", asks for a PRD/spec/technical doc, or is setting up a new project and about to scaffold docs. Cuts doc count to the minimum that survives contact with reality.
---

# Doc Triage

Default answer to "should we write this doc?" is **no**. Only write what will be updated.

## Decision table

| Doc | Verdict | Instead |
|---|---|---|
| PRD | Keep. Only doc that answers *why + what*. | — |
| TRD | Merge into PRD or `ADR/` | one ADR file per irreversible decision |
| AFD | Merge into PRD as a "Flow" section | — |
| DBD (design brief) | Drop unless a designer exists | designer writes it, not devs |
| BSD (schema doc) | Drop | migrations / `schema.sql` are the truth |
| IPD (impl plan) | Drop | issue tracker / todo list |

## Size the suite

- Solo or 2 people → `README.md` + `schema.sql`. Nothing else.
- 3–8 people, or external client → `PRD.md` + `ADR/NNN-title.md`.
- Enterprise / audit / regulated → add formal TRD. Only then.

## Rules

- A doc not updated is a liability. N docs = N places to go stale.
- Schema and plans live in code and tickets. Duplicating them into prose guarantees drift.
- Decisions get ADRs (immutable, dated). Requirements get PRD (living). Never mix.
- Ask team size and "external client or not" before recommending anything.

## Minimal PRD skeleton

```markdown
# <Product>
## Problem
## Users
## Scope (in / out)
## Flows        <!-- replaces AFD -->
## Requirements <!-- numbered, testable -->
## Open questions
```

## ADR skeleton

```markdown
# NNN. <Decision>
Status: accepted | superseded by NNN
Context: <forces>
Decision: <what>
Consequences: <what we lose>
```

Deliberate skip: no templates directory, no doc-lint script. Add when the team grows past 8 or docs start drifting.
