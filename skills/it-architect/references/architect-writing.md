# IT Solutions Architect — writing bar

Canonical bar for **ADRs, options analyses, implementation plans, architecture reviews,
and decision gates**. Profession: **Solutions Architect** (IT/technical systems).
Optional estate framing: `ea-lite.md`.

Diagrams are supporting evidence (`architecture-diagram`); **decisions in prose are SoT**.

---

## Voice

- Senior SA talking to a sharp peer and to future-you — not a slide deck, not a textbook
- Plain language first; define jargon once
- Decisive: pick and defend; rank options honestly
- Fair: label assumptions; separate verified vs unverified
- Concise by default; long only when blast radius demands it
- Corrections: when a "fact" was wrong, fix the table and note what still stands

## Non-negotiables

1. **Problem / constraint first** — who hurts, what must be true, hard limits (hardware, security, ops ownership).
2. **Evidence** — prefer disk-verified, runtime-verified, or cited live config.
3. **Unverified table** — anything not proven stays out of "Decision" premises.
4. **Numbered decisions (D1…)** — each with a clear reject path where relevant.
5. **Alternatives** — short table: option → why not (or why second).
6. **Non-goals** — what this deliberately does not solve.
7. **Phases** — P0 often protects existing value before new capability.
8. **Open questions = gates** — owner + what is blocked.
9. **Runtime / scope clarity** — authoring surface vs production runtime vs target node (easy to conflate).
10. **Safety** — no secrets, tokens, private URLs, or credential material in the artifact.
11. **Depth proportional to blast radius** — see guide below.
12. **Shorten on edit** — new facts replace prose; do not sediment forever.
13. **Diagrams on every ADR** — ship **both**:
    - **Markdown flowchart** (Mermaid preferred): embed in the ADR and keep a sibling `.mmd` under a `diagrams/` folder next to the ADR when the repo has one.
    - **diagrams.net (draw.io)** `.drawio` XML: same topology, openable in [app.diagrams.net](https://app.diagrams.net) or the Draw.io editor extension.
    - **Object legend + edge legend** in the ADR: every box, zone, and arrow style named and defined (what / where / notes). Labels on shapes must be readable without hovering.
    - Keep Mermaid and draw.io **name-aligned** when components rename; prose Dn remains SoT if they drift.

## Depth guide

| Blast radius | Artifact |
|--------------|----------|
| Small, local, reversible | Short options note or concise ADR |
| Multi-component, security, data, always-on, billing-adjacent | Heavy ADR + plan; verified/unverified tables |
| Multi-capability / org-ish portfolio | SA core + optional EA-lite capability map |
| Typo / rename only | Do not ADR |

## Status lifecycle

`Proposed` → gates answered → `Accepted` → implement (or explicit spike-while-Proposed) → `Superseded` when replaced.

## Header fields (ADR)

| Field | Intent |
|-------|--------|
| Status | Proposed / Accepted / Superseded / Deprecated |
| Date | ISO or local date + rev if needed |
| Owner | Human owner |
| Runtime | Where it runs (profile, host, account) |
| Horizon | V1 scope vs later |
| Supersedes / Incorporates | Prior docs |
| Plan | Link/path to plan if separate |

## Decision quality checklist

- [ ] Each Di is implementable or explicitly a principle
- [ ] At least one rejected alternative with reason (or "no viable alternative")
- [ ] Feasibility called out (or blocked)
- [ ] Security/privacy implications not hand-waved
- [ ] Success policy / acceptance test idea when ops-facing

## Anti-patterns

- Architecture astronomy (views forever, no D1)
- "Best practice" with no constraint fit
- Guide copy-paste treated as live inventory
- Silent scope creep past Accepted
- P0 = shiny feature while backups/secrets unprotected
- EA full metamodel on a single integration
- Invented metrics or "verified" without a check
- Secrets "just for the ADR"

## Worked method (structure only)

Good internal patterns (do not paste secrets if publishing):

- Tight ops ADR: tiered decisions, single transport, success policy, non-goals
- Heavy platform ADR: live audit table, unverified table, D1–Dn, tiers, P0 protect-first, open gates

Copy the **method**, not host-specific facts, into new work.

## Completion criteria

- [ ] Reader can restate the decision in one breath
- [ ] Can see what was rejected and why
- [ ] Knows what is blocked on whom
- [ ] Knows where the file lives
- [ ] No secrets
- [ ] Markdown flowchart present (Mermaid embed + `.mmd` when repo has `diagrams/`)
- [ ] diagrams.net `.drawio` present and openable
- [ ] Object legend + edge legend define every visible shape/arrow
