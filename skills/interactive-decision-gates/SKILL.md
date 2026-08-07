---
name: interactive-decision-gates
description: "Use when multi-option gates, ADR Qs, or choice menus."
version: 1.0.0
author: ATtheGR8 & Hermes Agent
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [decisions, menus, gates, ADR, discuss-then-apply]
    related_skills: [universal-agent-work-sop, it-architect, plan]
---
<!-- skill: interactive-decision-gates — Use when multi-option gates, ADR Qs, or choice menus. -->

# Interactive decision gates

**Credits:** ATtheGR8 & Hermes Agent (co-created). Maintained by ATtheGR8. Copyright (c) 2026 Avery Thompson. **Not** an official Nous Research / Hermes product skill.

## When to use

- Resuming a **Proposed** ADR / plan to clear open questions
- Any discuss-then-apply menu with ranked options (security, install, backup, provider, fix paths)
- Any surface where the user picks among numbered options (Desktop, CLI/TUI, Discord, gateway chat, etc.)
- Surfaces where `clarify` / chip UI may **truncate** choice rows — body text is still required
- User challenges “why is X recommended over Y?” or “menu doesn’t match recommend”
- Soft nested forks inside a single row (“and maybe”, and/or, optionally, parenthetical alts)

Related (**when installed**): `universal-agent-work-sop` (pair-load on apply of the chosen path), `it-architect` / ADR stub (load the real architecture skill), continuity/handoff skill (read handoff first).

## Fully determined option IDs (mandatory)

**Every option ID must encode a complete next action.** Picking `N` alone must leave nothing ambiguous for the agent.

| Bad (conditional / process prose) | Good (fully determined) |
|---|---|
| “Accept only after revise” | **R)** Revise ADR+plan+runbook **now** · **A)** Accept revised design · **H)** Hold |
| “Do X after Y” as one pick | Separate IDs for Y-now vs X-when-ready |
| “1 or maybe also 2” | **1** only · **2** only · **3** = 1+2 |

- A pick of **process order** (“only after…”) is **not** authority to perform the intermediate mutate unless that row’s text is an explicit **do-it-now** action.
- After locks: if the next step needs umbrella+specialist apply, **re-load** `universal-agent-work-sop` + domain specialist before mutating.
## Decision ranking (mandatory)

**Always recommend the practical/secure (correct) option after verifying the rank.**  
Do **not** pick “recommended” for smallest-commit convenience, Q-label purity, or ease of saying yes.

| Prefer | Do not crown “recommended” only because |
|--------|------------------------------------------|
| Security + correctness | Fewest words / fewest sub-bullets |
| Cheap supersets (rotate **+** perms audit) when strictly better | Splitting related hygiene to look simpler |
| Architecture reliability (SQLite-safe backup, VPN split-tunnel for lab nets) | Defer with known residual risk and no upside |
| Honest “timing vs quality” when 1 vs 2 are equal quality | Fake total order |
| **Minimum that fixes the stated bug** when extras are optional hygiene | Bundling optional work into “the fix” so the menu omits the real recommendation |

**Mid-stream error handling:** if the user asks why N > M and M is safer or a superset, **admit the mis-rank, re-rank, and fix the recommendation in the same turn** — including rewriting the choice menu so it matches.

## Menu ↔ recommendation alignment (all surfaces — mandatory)

**Failure mode this blocks:** analysis ranks **(1) only**, closing line offers only **(1)+(2)** or **(2) only** — user cannot pick the recommendation.

**Rule: choice menu ≡ ranked decision space. Recommended ∈ menu under the same ID.**

1. Number options **1 / 2 / 3 / 4** with **full option text in the message body** (every surface).
2. Mark **Recommended: N** using that same number — not a prose-only “I recommend X” that is missing from the list.
3. **Combos** (e.g. 1+2) get their **own** number. Mark a combo “recommended” only if the rank says the combo is best — never because it “feels complete.”
4. **Optional hygiene** stays optional: separate number, or a combo row explicitly labeled *not required for the bug/fix*.
5. **No nested unresolved forks inside one row.** Forbidden in a recommended (or any) option:
   - “exclude A **and maybe** B”
   - “do X **and/or** Y”
   - “Z, **optionally** also W” when W is not already decided
   - parenthetical alts that change what gets applied (“A (or B on secondaries)”)
   - **conditional sequencing as the only row** (“Accept only after revise”, “apply after Accept”) without separate do-now IDs
   **Fix:** split into separate numbered options, give the combo its **own** `#`, or write **“B not included”** so picking that ID is fully determined.
6. **Self-check before send** (fail = rewrite before the user sees it):
   - [ ] Recommended path appears as a pickable numbered option
   - [ ] Every offered choice was actually ranked (no surprise bundles)
   - [ ] No orphan recommendation (recommend A while menu is only A+B / B)
   - [ ] **If the user picks only the recommended ID, every included path is fully determined** (no leftover maybe/optionally/or/only-after)
   - [ ] Conditional gates are split into **revise-now / accept / hold / apply** (or equivalent) IDs
7. If you re-rank mid-thread, **rebuild the menu in the same turn**.

Template:

```
Options:
1) …     ← Recommended (fixes <stated problem>)
2) …     ← optional / different tradeoff
3) …     ← workaround
4) …     ← out / never

Reply with 1–4.
```

## Presentation (surface-agnostic)

1. **Body prose is source of truth** for option text + numbers on **all** surfaces (Desktop, CLI/TUI, Discord, gateway, etc.).
2. User replies with a number (or short mix). Do **not** rely on `clarify` chips / buttons alone — they may truncate or omit full text.
3. **High-stakes gates (apply/sync/destruct):** prefer **body menus + number replies**; chips/`clarify` optional. If chips are used, body still carries full 1/2/3 text with the same IDs.
4. Optional: still call `clarify` for UX where available; free-text while multi-choice is pending does **not** resolve the gate (user must type `1`–`N` or `/stop`).
5. After each lock: short **gates locked so far** table + still-open + next move.

Discord/gateway note: clarify/chip rows often truncate — full text in body is non-negotiable there, but the same body-first rule applies on every surface.

## Gate-walk procedure

1. Load handoff/ADR (or task brief) when available. **Do not restart** finished audits.
2. Identify **blocking** gates vs deferrable.
3. Walk one gate (or orthogonal pair) at a time unless user asks one-pass.
4. For each gate:
   - State what it controls and what it does **not**
   - Separate **orthogonal knobs** (e.g. chat injection vs cron memory context) before asking
   - Table of options + **pre-verified** recommended
   - Proceed menu that **includes** the recommended ID (alignment rule above)
   - Lock intent vs apply when discuss-then-apply applies
5. Allow **staged locks**: principle now, host/parameter at later phase — better than leaving bad defaults open or forcing unchoosable picks.
6. Stop at natural break or continue per user (remaining Qs / runbook / execute).

## Pitfalls

- Conflating independent knobs into one false choice
- Recommend “A only” when “A+B” is cheap and strictly better — **or** the inverse: recommend “A only” then only offer “A+B”
- Closing menus that omit the recommended path
- Bundling optional hygiene into the only “fix” choice
- **Soft nested forks** in one recommended row (“and maybe”, and/or, optionally, parenthetical alts) left unlocked
- **Conditional-only options** (“Accept only after revise”) that the agent interprets as revise/apply authority
- Silent execute after “approve design”
- Re-litigating locked handoff decisions during gate-walk
- Clarify/chip-only options (any surface)
- Defending a weak “recommended” after user correctly challenges it
- Writing Discord-only procedures when the same failure hits Desktop/CLI
- Applying the chosen path without re-loading `universal-agent-work-sop` + domain specialist when the pick is a mutate

## Completion

- [ ] Each offered “recommended” survived a security/correctness rank check
- [ ] **Recommended ∈ numbered choices with the same ID** (alignment self-check)
- [ ] **No unresolved nested forks** inside any offered row (pick ID ⇒ fully determined apply set)
- [ ] **No conditional-only IDs** without a matching do-now option when intermediate work is intended
- [ ] Options fully readable in message body on the active surface
- [ ] Locks recorded; apply deferred until user says execute (unless they ordered now)
- [ ] Orthogonal concerns explained when user compares mixes
