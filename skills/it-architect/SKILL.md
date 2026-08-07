---
name: it-architect
description: "Use when IT/systems architecture, ADRs, or design reviews."
version: 1.2.0
author: ATtheGR8 & Hermes Agent
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [Architecture, ADR, Solutions-Architect, IT, Design, Planning]
    related_skills: [universal-agent-work-sop, architecture-diagram, github-expert-writing, interactive-decision-gates, plan, architecture-adr]
---
<!-- skill: it-architect — IT/systems architecture, ADRs, plans, reviews. -->

# IT Solutions Architect (`it-architect`)

**Solutions Architect** practice for IT / technical systems (infra, integration, security,
platforms, multi-node, cloud/netsec-class decisions). Optional **EA-lite** when estate-level
framing helps. Not a TOGAF course; not a pure code-feature blueprint skill.

**Credits:** ATtheGR8 & Hermes Agent (co-created). Maintained by ATtheGR8. Copyright (c) 2026 Avery Thompson. **Not** an official Nous Research / Hermes product skill.

## When to use

Load **before** drafting:

- Architecture Decision Records (new project or non-trivial technical decision)
- Options analysis / recommendation with rejected paths
- Implementation plans tied to an ADR
- Architecture review of an existing design or "is this still valid?"
- Decision gates for the user (ranked choices; full option text in body as 1/2/3)
- Optional: capability map / view framing (EA-lite) for multi-capability or enterprise audience
- **Revise** of an existing ADR / multi-file design package (ADR + plan + runbook + diagrams)

**Always ask** whether an ADR is wanted when a new project is identified (unless already ordered).

**Do not use for:** `gh` lifecycle prose → `github-expert-writing`; pretty diagrams only →
`architecture-diagram`; pure code class design / feature file maps without systems scope.

## Required load sequence

**Before the first mutation** of any ADR/plan/runbook/diagram in this turn:

0. `skill_view(name='universal-agent-work-sop')` — umbrella triage/gate/verify (**required**; not optional)
1. `skill_view(name='it-architect')` — this file
2. `skill_view(name='it-architect', file_path='references/architect-writing.md')` — full bar
3. Matching template under `templates/`
4. If estate/portfolio framing needed: `references/ea-lite.md` + optional `templates/capability-map.md`
5. If user choice is needed: load `interactive-decision-gates` (fully determined option IDs)
6. Draft → completion criteria → path to user; preserve status (**Proposed** until Accept; do not auto-Accept or auto-Apply)

`architecture-adr` is a **stub redirect** to this skill — if it surfaces, still run steps 0–2; never stop at the stub.

## Non-negotiables (summary)

- **SA core:** problem and constraints first; numbered decisions; rejected alternatives explicit
- **Evidence:** live/disk-verified facts vs **explicitly unverified** — never conflate
- **Feasibility + security before cleverness**; stop if not feasible/secure and say so
- **Non-goals** and **supersedes** when replacing a prior design
- **Depth proportional to blast radius** (small change → short note; platform/security/data → heavy ADR)
- **Open questions are gates** — do not pretend implementation is unblocked
- **Edits should shorten** when possible; no essay without a decision
- **No secrets** in ADRs (IDs, tokens, webhooks, keys)
- **Diagrams (required on every ADR):** (1) markdown flowchart — Mermaid preferred, checked in as `.mmd` and embedded in the ADR; (2) **diagrams.net / draw.io** `.drawio` XML (editable in app.diagrams.net or VS Code Draw.io). Include a shared **object legend** and **edge legend** so every box/zone/arrow meaning is explicit and visible. Prose decisions remain SoT; diagrams stay consistent with Dn.
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

That name is a **stub** that redirects here. Prefer `it-architect` for all new work. If the stub loads first: still pair-load `universal-agent-work-sop` + this skill before mutating.

## Decision propagation (on revise / Accept prep)

When a lock changes in the **canonical ADR**, check dependents in the same work package before calling done:

| Layer | Action |
|---|---|
| Canonical ADR | Update decision table + normative text + changelog; status only changes on owner order |
| Plan / runbook / checklists | Align locks, phases, verify/rollback rows |
| Diagrams (`.mmd` / embedded Mermaid / `.drawio`) | Same identity/path labels as prose |
| Session handoff (if used) | Point at revised status; do not invent Accept |

**Done when:** old superseded wording is gone from the package (or explicitly marked superseded), and **Proposed ≠ Accepted ≠ Applied** stays coherent.

## Diagram verification

- Text/grep of labels is a **minimum** consistency check.
- For high-blast or user-facing design review: open/export check or vision pass when available — do not claim full visual QA from grep alone.

## Install note

Copy this folder into your Hermes skills tree (see skill README). Multi-profile sync is install-specific and out of scope for this public skill.

## Completion before handoff

- [ ] `universal-agent-work-sop` loaded on this mutate/draft turn
- [ ] Decision (or ranked recommendation) clear in about one screen for concise; heavy still leads with decisions
- [ ] Verified vs unverified separated when claims depend on environment
- [ ] Non-goals + open questions listed or explicitly none
- [ ] Path to artifact given; status **Proposed** until accepted (never silent Accept/Apply)
- [ ] Decision propagation checked when revising locks (ADR → plan/runbook/diagrams)
- [ ] No secrets
- [ ] ADR diagrams: Mermaid (or equivalent) flowchart embedded + `.mmd` when repo has `diagrams/`
- [ ] ADR diagrams: diagrams.net `.drawio` present and openable
- [ ] Object legend + edge legend define every visible shape/arrow

## Common pitfalls

1. Essay context with no decision table
2. Treating search misses or guides as live fact
3. Skipping rejected alternatives
4. Implementing through open gates without explicit spike permission
5. Using full EA ceremony on a single-service ADR
6. Putting tokens, webhook URLs, or private channel IDs in the doc
7. **Mutating ADR packages without `universal-agent-work-sop`** (specialist-only / stub-only)
8. **Stopping at `architecture-adr` stub** without loading this skill’s body + writing bar
9. **Silent Accept or apply** after a design revise menu without a fully determined Accept/apply option
10. **Forgetting dependents** when a lock changes (plan/runbook/diagrams still say the old decision)
