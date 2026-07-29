# EA-lite (optional)

Thin enterprise-architecture **vocabulary** for Solutions Architects.
**Not** a TOGAF implementation. Use when the audience or scope is multi-capability,
standards, or portfolio — not for every service ADR.

## When to open this file

- Multiple capabilities or systems must stay coherent
- Stakeholder asks for "enterprise view" / interview / portfolio narrative
- You need a one-page **capability map** before diving into a single solution ADR
- Setting a **principle** that future ADRs must not violate

**Skip** for single-integration ADRs with clear owner and runtime (use SA core only).

## Views (use only what earns its keep)

| View | Question it answers | Typical SA artifact |
|------|---------------------|---------------------|
| **Business / capability** | What ability does the org/lab need? | Capability map row |
| **Application / system** | Which systems provide it? | Context diagram, integration list |
| **Technology** | Where does it run; what stack? | Runtime row in ADR header, tech decision Di |
| **Security** | Who trusts whom; what is exposed? | Threat/constraint table, P0 harden |
| **Operations** | Who runs it; failure/alert path? | Success policy, runbooks, ADR ops tiers |

One ADR usually spans 2–3 views. Name them in Context if helpful; do not force all five.

## Principles (keep a short house list)

Write 3–7 principles max when needed, e.g.:

- Local/loopback before cloud for high-sensitivity derivers
- Protect existing state (backup) before new capability
- One transport for a given ops path unless proven broken
- Profile/runtime ownership is explicit (no silent multi-token)

Principles constrain future Ds; they are not a substitute for a decision.

## Capability map (optional template)

See `templates/capability-map.md`.

Columns that matter: **Capability → System/component → Owner → Runtime → Maturity → Notes**.
Maturity examples: absent / spike / production / deprecated.

## Anti-patterns

- Full ADM phase gates for a home-lab change
- Capability map with no owner or runtime
- "As an EA…" filler with no map and no decision
- Duplicating the entire ADR inside every view

## Return path

After EA-lite framing, **drop back to SA core**: ADR / options / plan with evidence and gates.
