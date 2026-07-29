---
name: it-architect
description: "Use when IT/systems architecture, ADRs, or design reviews."
version: 1.0.0
author: ATtheGR8 & Hermes Agent
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [Architecture, ADR, Solutions-Architect, IT, Design, Planning]
    related_skills: [architecture-diagram, github-expert-writing, plan]
---
<!-- skill: it-architect — IT/systems architecture, ADRs, plans, reviews. -->

# IT Solutions Architect (`it-architect`)

**Solutions Architect** practice for IT / technical systems (infra, integration, security,
platforms, multi-node, cloud/netsec-class decisions). Optional **EA-lite** when estate-level
framing helps. Not a TOGAF course; not a pure code-feature blueprint skill.

**Credits:** ATtheGR8 & Hermes Agent (co-created). Maintained by ATtheGR8. Copyright (c) 2026 Avery Thompson. Not an official Nous Research / Hermes product skill.

## When to use

Load **before** drafting:

- Architecture Decision Records (new project or non-trivial technical decision)
- Options analysis / recommendation with rejected paths
- Implementation plans tied to an ADR
- Architecture review of an existing design or "is this still valid?"
- Decision gates for the user (ranked choices, reply 1/2/3)
- Optional: capability map / view framing (EA-lite) for multi-capability or enterprise audience

**Always ask** whether an ADR is wanted when a new project is identified (unless already ordered).

**Do not use for:** `gh` lifecycle prose → `github-expert-writing`; pretty diagrams only →
`architecture-diagram`; pure code class design / feature file maps without systems scope.

## Required load sequence

1. `skill_view(name='it-architect')` — this file
2. `skill_view(name='it-architect', file_path='references/architect-writing.md')` — full bar
3. Matching template under `templates/`
4. If estate/portfolio framing needed: `references/ea-lite.md` + optional `templates/capability-map.md`
5. Draft → completion criteria → path to user; **Proposed** until gates answered

## Non-negotiables (summary)

- **SA core:** problem and constraints first; numbered decisions; rejected alternatives explicit
- **Evidence:** live/disk-verified facts vs **explicitly unverified** — never conflate
- **Feasibility + security before cleverness**; stop if not feasible/secure and say so
- **Non-goals** and **supersedes** when replacing a prior design
- **Depth proportional to blast radius** (small change → short note; platform/security/data → heavy ADR)
- **Open questions are gates** — do not pretend implementation is unblocked
- **Edits should shorten** when possible; no essay without a decision
- **No secrets** in ADRs (IDs, tokens, webhooks, keys)
- **EA-lite is optional** — default path is SA ADR/plan/review

## Genre → template

| Genre | When | `file_path` |
|-------|------|-------------|
| ADR (concise) | Default decision record | `templates/adr.md` |
| ADR (heavy) | High blast radius / multi-system | `templates/adr-heavy.md` |
| Options analysis | Choose among approaches before ADR lock | `templates/options-analysis.md` |
| Implementation plan | After or with ADR, build phases | `templates/implementation-plan.md` |
| Architecture review | Audit existing design vs live state | `templates/architecture-review.md` |
| Decision gates | User must answer before proceed | `templates/decision-gates.md` |
| Capability map | EA-lite / portfolio | `templates/capability-map.md` |

## Relationship to `architecture-adr`

If your install still has a thin `architecture-adr` skill, treat it as a redirect here.
Prefer **`it-architect`** for all new architecture work.

## Maintenance

- Source of truth for the **public** package: this git repository
- Improve via PR/commit; copy into `~/.hermes/skills/` (or a profile skills dir) to use
- Prefer not forking the bar into unrelated bundled skills

## Completion before handoff

- [ ] Decision (or ranked recommendation) clear in about one screen for concise; heavy still leads with decisions
- [ ] Verified vs unverified separated when claims depend on environment
- [ ] Non-goals + open questions listed or explicitly none
- [ ] Path to artifact given; status **Proposed** until accepted
- [ ] No secrets

## Common pitfalls

1. Essay context with no decision table
2. Treating search misses or guides as live fact
3. Skipping rejected alternatives
4. Implementing through open gates without explicit spike permission
5. Using full EA ceremony on a single-service ADR
6. Putting tokens, webhook URLs, or private channel IDs in the doc
