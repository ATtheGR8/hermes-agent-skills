---
name: agent-memory-budget
description: "Use when agent memory is near cap or needs compression."
version: 1.0.0
author: ATtheGR8 & Hermes Agent
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [agent, memory, budget, compression, limits, retention]
    related_skills:
      - agent-knowledge-review
      - universal-agent-work-sop
---
<!-- skill: agent-memory-budget — Memory pressure: inventory, compress, or raise. -->

# Agent memory budget

**Credits:** ATtheGR8 & Hermes Agent (co-created). Maintained by ATtheGR8.
Copyright (c) 2026 Avery Thompson. **Not** an official Nous Research / Hermes
product skill.

**Memory budget** means managing finite always-on context for an agent —
measuring pressure, preferring non-destructive fixes, compressing **without
silent semantic loss**, relocating misplaced content, and raising capacity only
after inventory and explicit human approval.

This skill is framework-neutral. It assumes some bounded store(s) for durable
agent notes (often split into “who the user is” vs “environment / ops facts”).
Platform details live in **Hermes adaptation**.

Pairs with `agent-knowledge-review` for keep/reject/destination decisions on
staged or proposed writes. Use that skill first when the queue is full of
low-value candidates; use **this** skill when retained material still will not
fit or a live line must be safely shortened.

## When to use

- Always-on memory or user-profile text is near its character (or token) limit
- A write failed or would fail because of the cap
- The human asks whether to **tighten (compress)** vs **raise limits**
- Planning a replace that shortens or merges existing durable lines
- Multi-copy / multi-profile memory drifts or merge conflicts after edits

**Don't use for:** deciding whether a one-off fact should exist at all →
`agent-knowledge-review`; full procedure authoring → a domain skill; dumping
task progress or PR logs into memory “to save tokens elsewhere.”

## Purpose

Caps exist so always-on context stays loadable and high-signal. Bad responses to
pressure:

1. **Silent drop** of the longer or more precise entry when two copies differ
2. **Density-only shaving** that preserves word count “theme” but kills steer
3. **Blind limit raises** that skip inventory and entrench junk
4. **Second adds** of near-duplicates instead of replace/merge

This skill enforces: **measure → inventory → non-limit fixes → per-entry gate →
human OK → apply → verify**. Over-limit packing should **fail closed** when the
tooling can do so — never invent a shorter-wins policy that destroys meaning.

## Stores (generic)

Name them clearly in every review:

| Store | Typical content |
|--|--|
| **User profile** | Stable human prefs, style, non-negotiables |
| **Operational memory** | Host/tool locks, environment facts, short pointers to skills |
| **Other always-on** | Only if the host has more blocks — treat each as its own budget |

Procedures and runbooks belong in **skills**, not in these stores. Memory may
hold a **one-line pointer** (“Load skill `X` when …”).

## Procedure

### 1. Measure

**Done when:** each store has used / limit / free (and free%), plus pending bulk
if a queue exists.

Prefer the same length function the runtime uses (often Python `len(text)` on the
canonical file or store API). Do not trust raw byte counts if the runtime counts
characters.

Also note:

- whether the next desired write is **add** vs **replace/merge**
- count of staged candidates (skip archives/backups)
- whether multiple copies of the store must stay identical

### 2. Pressure bands

Use the **worse** of percent free and absolute free **per store**. Thresholds
below are **starting defaults** — adjust to the host’s real limits, but keep the
band *meanings*.

| Band | Default when (either) | Bias |
|--|--|--|
| **Green** | free ≥ ~15% **and** free is comfortably above a small absolute floor | Normal add/replace after ordinary review |
| **Yellow** | free ≤ ~15% **or** absolute free is tight | Prefer replace/merge; offer light compress |
| **Red** | free ≪ 5% **or** absolute free critical **or** over-limit write failed | Compress/replace/reject before new adds; raise only after inventory + explicit OK |

State the band in the recommendation. Do not raise limits from Green boredom.

### 3. Prefer non-limit fixes first

**Done when:** every cheaper fix is considered before a raise.

1. **Reject** low-value staged candidates (`agent-knowledge-review`)
2. **Replace** refinements instead of second add
3. **Merge** true same-domain overlap carefully
4. **Relocate** runbooks → skills; leave pointers only
5. **Drop** dead/false lines with human OK
6. **Tighten** only lines that pass the per-entry gate below

### 3a. Per-entry compress gate (mandatory)

Before any existing line enters a compress/replace **pack**, answer all three.
Put pass/fail in the review table — not only after pushback.

#### Q1 — Why would we edit this?

| Acceptable (non-exclusive) | Not sufficient alone |
|--|--|
| **Refine** the same fact (stale number, wrong slogan, clearer lock) | “It’s long” |
| **Dedupe / merge** true overlap | “We need free chars” |
| **Wrong layer** (runbook → skill; task log → handoff) | Density for its own sake |
| **Dead / false** content | |

If the only honest answer is the character limit → **leave the line**. Free
space elsewhere, reject the incoming add, or consider a raise.

#### Q2 — Do any edits reduce effectiveness or skill invocation?

Check explicitly:

- **Skill name** still present when the line is a load pointer
- **Load / when-to-use scope** still true (e.g. “for all agent work”)
- **Decision force** intact (locks, never/always, menu rules)
- **Protected topic?** — security, auth routing, backup/restore pointers,
  “never do X” locks: default **no density edit**; only refine/correct

Fail Q2 → drop from pack or rewrite until it passes. “Skill name still there”
is not enough if scope or force was gutted.

#### Q3 — If we only had room for one keep — is this it?

Ranking check. If **yes**, do not density-shave it; keep full steer and free
space on other lines, reject adds, or raise.

**Pack rule:** every proposed before→after must pass Q1–Q3. Present failed
candidates as **excluded** with a one-line reason.

### 4. Recommend compress vs raise

**Done when:** the human can pick a fully determined plan.

Present:

| Entry lead | Store | Q1 | Q2 | Q3 | Action | Before → after (if edit) |
|--|--|--|--|--|--|--|

Then a single recommended plan, for example:

- **Compress pack A** (N lines) + reject M staged adds — no raise
- **Relocate** two runbooks to skills, then light compress
- **Raise** store S to new_limit after inventory proves essentials still overflow

**Raise limits only if:**

1. Inventory is done and named essentials still do not fit
2. Human explicitly picks raise + the new cap values
3. Config/runtime limits are updated everywhere those stores are enforced
4. Content identity across copies is restored if you edited text too

**Do not** raise limits to skip inventory or to avoid saying no to junk.

### 5. Apply after explicit OK

- Apply replaces/merges/removes with the host’s store API or file discipline
- Prefer one intentional source of truth, then copy
- **Never discard staged candidates after failed apply**
- If tooling offers batch apply, remember batches may be **single-store** —
  split user-profile vs operational memory into separate applies when required

### 6. Multi-copy / sync discipline

When several profiles, machines, or mirrors must share the same always-on text:

1. Edit **one** intentional copy (or apply one approved op set)
2. **Identity-copy** the full store files to all peers **before** any automated
   merge that might prefer a different sibling
3. Run merge/sync dry-run if available
4. Verify equal hashes (or equivalent) and spot-check key phrases

**Anti-patterns:**

- Lengthen on copy A, leave short text on B/C, run “sync” that resolves
  near-dupes by **keeping the shorter** → precise wording vanishes
- Over-limit union packed by silently dropping entries → prefer **fail closed**
  with a loud report
- Divergent unique tokens in two “same topic” lines resolved without human pick
  → prefer **conflict** over silent merge

If you control the merger: longer/superset can win for pure containment; if both
sides have unique substance, **stop and ask**.

### 7. Verify

**Done when:**

- measured used/limit/free match the plan’s expected band
- every kept high-value phrase still present
- excluded Q1–Q3 lines were not silently edited
- multi-copy stores match when shared
- no staged candidate was discarded on failure

## Worked examples (synthetic)

### A — Yellow band, replace not add

- Operational memory 90% full
- Staged add repeats an auth routing lock with one new clause
- **Plan:** replace the live line with the refined sentence; reject the add as
  written; no raise

### B — Density shave fails Q2

- Proposal shortens “Work SOP: skill `universal-agent-work-sop` — for all agent
  work; triage; verify before done” to “Use work SOP skill”
- **Q2 fail:** load scope and force gutted
- **Exclude** from pack; free space elsewhere

### C — Raise after honest inventory

- User profile at red; remaining lines are all Q3 “must keep” prefs
- No staged junk; skills already hold procedures
- **Plan:** raise user-profile cap to an agreed value; verify runtime config;
  do not compress protected prefs

### D — Wrong layer

- 15-line restart procedure in operational memory
- **Plan:** move to skill `service-restart`; leave one pointer line; measure again
  before any raise

## Common pitfalls

1. Raising limits before inventory
2. Shorter-near-dupe-wins across copies after a one-sided lengthen
3. Density-only edits of protected or skill-pointer lines
4. Compress packs without per-entry Q1–Q3 in the table
5. Second adds instead of replace
6. Mini-runbooks left in memory to “save a skill file”
7. Using byte-oriented `wc` when the runtime counts characters
8. Treating sync failure noise (notifications) as merge failure — read the merge
   report itself
9. Mixed-store batches when the API is single-target
10. Claiming success without re-measure and key-phrase checks

## Verification checklist

- [ ] Used/limit/free (and band) stated per store
- [ ] Pending/low-value candidates filtered (`agent-knowledge-review` as needed)
- [ ] Non-limit fixes considered before raise
- [ ] Every compress candidate has Q1 / Q2 / Q3
- [ ] Excluded lines listed with reasons
- [ ] Human OK before destructive drops or limit changes
- [ ] Applies verified; no discard-on-failure
- [ ] Multi-copy identity checked when shared stores exist
- [ ] Post-change measure confirms expected headroom
- [ ] Key phrases / skill pointers still present

## Hermes adaptation

| This skill | Hermes |
|--|--|
| User profile store | `USER.md` / `user_char_limit` |
| Operational memory store | `MEMORY.md` / `memory_char_limit` |
| Measure | On-disk lengths or `load_on_disk_store()` usage — not bare default store objects with wrong caps |
| Staged writes | `pending/memory/` when memory write approval is on |
| Offline apply | Host apply helpers with correct `HERMES_HOME`; success before discard |
| Shared profiles | Identity-copy `MEMORY.md`/`USER.md` to all profiles that share memory, then sync |
| Sync policy (recommended) | Hybrid near-dupe (longer/superset; conflict on divergent unique tokens); **fail closed** when over limit after dedupe — no silent shorter-first pack |

Notes:

- Verify **live** config caps; do not assume any blog default.
- Daily or cron sync is not a substitute for identity-copy after lengthening one
  profile.
- Skill trees are **not** memory sync — distribute skills separately.
- Private estate scripts and host names stay out of this public skill.

**Not official Nous guidance** — community method developed while operating Hermes.
