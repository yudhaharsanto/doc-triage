# Doc Triage

A skill that decides which project documents actually need to exist.

Ask an AI agent "do we need a PRD, TRD, AFD, DBD, BSD, and IPD?" and most will happily scaffold six folders of templates. Six documents means six places to go stale, and nobody updates six documents.

Doc Triage answers with the minimum: usually one file.

## The default answer is no

| Doc | Verdict | Instead |
|---|---|---|
| **PRD** | Keep. The only doc that answers *why + what*. | — |
| **TRD** | Merge into PRD, or `ADR/` | one ADR per irreversible decision |
| **AFD** (app flow) | Merge into PRD as a "Flows" section | — |
| **DBD** (design brief) | Drop unless a designer exists | the designer writes it, not devs |
| **BSD** (schema doc) | Drop | migrations / `schema.sql` are the truth |
| **IPD** (impl plan) | Drop | the issue tracker is the plan |

Schema documents and implementation plans duplicate code and tickets. Duplicating them into prose guarantees drift.

## Size the suite

| Context | Documents |
|---|---|
| Solo or 2 people | `README.md` + `schema.sql`. Nothing else. |
| 3–8 people, or an external client | `PRD.md` + `ADR/NNN-title.md` |
| Enterprise / audit / regulated | add a formal TRD. Only then. |

## What it produces

Given a project, the skill writes only what the size justifies:

```markdown
# <Product>
## Problem
## Users
## Scope (in / out)
## Flows        <!-- replaces AFD -->
## Requirements <!-- numbered, testable -->
## Open questions
```

```markdown
# NNN. <Decision>
Status: accepted | superseded by NNN
Context: <forces>
Decision: <what>
Consequences: <what we lose>
```

## Install

```bash
# [CC]
git clone https://github.com/yudhaharsanto/doc-triage.git ~/.claude/skills/doc-triage

# OpenCode
git clone https://github.com/yudhaharsanto/doc-triage.git ~/.config/opencode/skills/doc-triage
```

Triggers on "do we need X doc", "write me a PRD/spec/technical doc", "set up project documentation", or a proposal for a multi-document suite.

## Rules it enforces

- A document nobody updates is a liability. N docs = N places to go stale.
- Decisions get ADRs — immutable, dated. Requirements get a PRD — living. Never mix the two.
- Ask team size and "external client or not" before recommending a suite.
- One file beats six. Always.

## Non-goals

No templates directory, no doc-lint script, no doc generator. The skeletons fit inline in `SKILL.md`. Revisit if a team grows past ~8 people or docs start drifting.

## License

MIT
