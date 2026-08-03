---
name: agent-knowledge-review
description: "Use when reviewing agent skills or memory for retention."
version: 1.0.0
author: ATtheGR8 & Hermes Agent
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [agent, knowledge, memory, skills, review, retention, governance]
    related_skills:
      - agent-memory-budget
      - universal-agent-work-sop
---
<!-- skill: agent-knowledge-review — Review agent skills/memory for durable retention. -->

# Agent knowledge review

**Credits:** ATtheGR8 & Hermes Agent (co-created). Maintained by ATtheGR8.
Copyright (c) 2026 Avery Thompson. **Not** an official Nous Research / Hermes
product skill.

**Knowledge review** means deciding whether a proposed or existing piece of
agent-facing material should become (or remain) **durable operating context**,
and if so **where** and **in what shape**.

This skill is framework-neutral. It applies to staged write queues, manual
audits, “should I remember this?” moments, skill hygiene passes, and similar
workflows in Hermes or other agent systems. Platform-specific plumbing lives in
**Hermes adaptation** at the end.

Pairs with `agent-memory-budget` when the question is capacity, compression, or
limit raises rather than keep/reject/destination.

## When to use

- Reviewing **proposed skills** or skill edits before they become permanent
- Reviewing **proposed memory / user-profile** writes before they become permanent
- Periodic hygiene of skills, always-on memory, or house rules
- An agent asks whether to “save,” “remember,” or “skill-ify” something
- Background or queue systems have staged candidates and a human must decide

**Don't use for:** pure capacity math and compress packs alone → load
`agent-memory-budget`; one-off project narrative that belongs in a handoff or
plan; authoring a brand-new skill from scratch without a retention decision
(use your skill-authoring workflow, then return here before permanent install).

## Purpose

Persistent agent systems fail in two opposite ways:

1. **Everything becomes permanent** — noise crowds out signal; context bloats;
   stale facts steer future work.
2. **Nothing durable is captured** — the same costly mistakes and preferences
   are rediscovered forever.

This skill enforces a third path: **curated durability**. Rejection is a
successful review outcome when the candidate fails the retention tests.

## Knowledge layers (destination map)

Before approve/reject, assign a destination. One candidate → one primary home.

| Layer | Holds | Examples | Does **not** hold |
|--|--|--|--|
| **User profile** | Who the human is; stable prefs and style that survive projects | “Prefer local over hosted,” “discuss-then-apply,” secret-handling prefs | Project outcomes, task logs, temporary paths |
| **Operational memory** | Environment facts, tool quirks, durable locks that steer many sessions | Host topology locks, auth routing quirks, “never X while Y is true” | Full runbooks, PR numbers, “we did X on date” |
| **Skills / procedures** | Reusable how-to with steps, checks, pitfalls | Review workflows, deploy playbooks, debug loops | One-line prefs; raw session dumps |
| **Project artifacts** | Time-bounded state for a live effort | Handoffs, ADRs, plans, issue trackers | Cross-project always-on context |
| **Session history** | Narrative and recoverability | Chat transcripts, search later | Anything that must steer *without* re-search |

**Rule of thumb:** if future agents need a **procedure**, write or patch a
**skill**. If they need a **compact lock or fact**, use operational memory. If
they need a **preference about the human**, use the user profile. If they only
need to **resume a project**, use a handoff or plan.

## Sustainment filter (keep vs reject)

Ask first:

> Will this still matter in roughly **90 days** if the originating project folder
> is cold?

**Keep only if at least one is true:**

1. **Reuse** — the procedure or fact will be needed outside this project’s active
   thread (another workspace, post-upgrade, outage, second host, later project).
2. **Steer** — without it, the agent will repeat a costly mistake or violate a
   hard preference.
3. **Long-lived lock** — placement, identity, or policy that must not drift while
   a system remains in the environment (including long-lived pilots).
4. **Cross-project** — applies to installs, reviews, or operations generally, not
   only this effort.

**Else → reject** (or redirect). Rejection is success.

| Redirect to | When |
|--|--|
| Handoff / project status | Open gates, resume state, project narrative |
| ADR / plan | Why A over B; durable decision for one system |
| Session history | Story that can be searched later; no always-on need |
| Skill patch (umbrella) | New near-duplicate of an existing procedure |
| Drop | Already live, pure noise, or false |

### Shape when keeping

- Prefer **patch an umbrella skill** over a second near-skill when the domain
  already has a home.
- Prefer **replace/refine** an existing memory or profile line over a second add.
- Skills: keep the **trigger description** short; put detail in the body.
- Memory: **one compressed lock line** — not a mini-runbook.
- Tag mentally: *pilot-while-live* vs *estate-permanent*; plan retire of
  pilot-only material when the system leaves (never silent delete of something
  still referenced).

## Procedure

### 1. Inventory (read-only)

**Done when:** every candidate is listed with enough gist to decide.

For each candidate note:

- identity (id, path, or title)
- action type (create / edit / add / replace / remove / batch)
- target layer (skill, user profile, operational memory, unknown)
- origin (agent proposal, background review, human request)
- gist of content
- age / mtime if available

Group by name or topic. Flag:

- **duplicate creates** for the same skill or same fact
- **already live** (same meaning already installed)
- **refines existing** (replace, don’t second-add)
- **mixed batch** that spans layers (split later)

Ignore applied archives and backup files if your system has them.

### 2. Classify destination

**Done when:** each candidate has a primary layer or “reject/redirect.”

Use the destination map. If a skill body is really a preference, reclassify.
If memory text is really a runbook, reclassify to skill (or reject the memory
form and author a skill instead).

### 3. Preflight (blocking before recommend-approve)

**Done when:** every keep-candidate has no open FAIL, or FAIL is explicitly
overridden by the human.

#### Skills — minimum preflight

| Check | FAIL if | Fix |
|--|--|--|
| Trigger description | Missing, vague, or too long for the host index | Shorten; trigger-first; end with `.` when local convention requires |
| Identity comment / title | Package has no stable human-readable one-liner | Add skill comment or README one-liner |
| Completeness | Stub, TODO-only, or empty body | Reject or hold |
| Duplicate pending/create | Two active creates for the same skill name | Keep newest useful package; reject older |
| Safety wording | Body looks like live secrets, wipe recipes, or scanner-bait examples | Reword; never teach guard bypass |
| Name collision | Create would clobber a different installed skill | Prefer patch/edit path |

**WARN (call out, don’t auto-block):** pilot-only scope; huge file trees;
home-domain vs global install intent; large unrelated diffs.

#### Memory / user profile — minimum preflight

| Check | FAIL if | Fix |
|--|--|--|
| Sustainment filter | Fails 90-day / reuse / steer / lock / cross-project | Reject or redirect |
| Already live | Same pref/fact already present | Reject pending; no re-add |
| Wrong op | Should be replace but proposed as add | Convert recommendation to replace |
| Runbook in memory | Multi-step procedure parked in always-on memory | Move to skill; memory keeps pointer only |
| Headroom | Add would blow cap with no budget plan | Load `agent-memory-budget` before approve |
| Live-line shorten | Replace shortens or densifies an existing line | Run budget **Q1–Q3** first (`agent-memory-budget`) |

### 4. Recommend (discuss-then-apply)

**Done when:** the human has a clear approve / reject / hold / redirect plan.

Present a table, not a wall of prose:

| Id / name | Layer | Filter | Preflight | Recommendation | Notes |
|--|--|--|--|--|--|

**Default pattern:**

1. Reject one-off / cold-in-90-days packages (handoff/ADR/session instead).
2. Reject duplicates and already-live facts.
3. Prefer umbrella skill patch over twin skill.
4. Prefer replace over second add for memory/profile.
5. Hold low-value or unclear items unless the human asks to force them.
6. If both a **procedure skill** and a **memory compress** are pending for the
   same domain, **approve the skill first** so the playbook is locked before
   memory is thinned.

State a single **recommended plan** first. Do **not** apply until explicit OK.

### 5. Apply — only after explicit human OK

**Done when:** every approved apply either succeeded with evidence, or failed
without destroying the candidate.

Rules:

- Apply only what was approved; partial approval ≠ full queue wipe.
- **Never discard a staged candidate after a failed apply** (data loss).
- Prefer path-based / API apply helpers over pasting full bodies into shell
  heredocs (host guards may false-positive on embedded text).
- Record success before cleanup of staging artifacts.

### 6. Verify

**Done when:** disk (or store) matches the plan and the queue matches intent.

- Approved skills exist at the expected install path with expected names.
- Approved memory/profile lines are present; rejected ones are absent.
- Queue empty or intentionally held items listed.
- If the install is multi-profile or multi-copy, shared stores match (see
  Hermes adaptation and `agent-memory-budget`).
- If global rollout was intended, note that **local apply ≠ estate ship** —
  manifest, sync, pin, or distribute as a separate explicit step.

## Worked examples (synthetic)

### A — Reject skill (one-off project)

**Candidate:** skill `acme-widget-deploy-2026` with steps for one customer cutover.

- 90-day test fails once the cutover folder is cold.
- Redirect: handoff + ADR for that project.
- **Recommend reject.** Do not immortalize the cutover as a global skill.

### B — Keep skill (cross-project)

**Candidate:** skill documenting staged-write review with preflight and
never-discard-on-failed-apply.

- Reuse + steer + cross-project all true.
- Preflight: short trigger description, complete body, no secrets.
- **Recommend approve** (and prefer this as umbrella if twins exist).

### C — Memory add → replace

**Candidate:** add “Prefer discuss-then-apply for consequential changes.”

- Live profile already has the same preference in different words.
- **Recommend reject add** or **replace** the live line if the new wording is
  strictly clearer — not a second bullet.

### D — Runbook parked in memory

**Candidate:** 12-line MEMORY entry with numbered restart steps.

- Wrong layer.
- **Recommend:** author/patch a skill; keep at most a one-line pointer in
  operational memory (“Restart playbook: skill `service-restart`”).

## Relationship to capacity work

| Situation | Skill |
|--|--|
| Keep / reject / destination / approve staged knowledge | **This skill** |
| Near cap, compress pack, raise limits, Q1–Q3 density gates | **`agent-memory-budget`** |
| Both at once | Run this skill’s filter first; send survivors that need thinning through budget |

## Common pitfalls

1. Approving because the debug was hard — hard ≠ reusable.
2. Treating every staged background proposal as worthy of permanence.
3. Second **add** when **replace** is correct.
4. Mini-runbooks in always-on memory instead of skills.
5. Twin skills for a pilot when an umbrella patch would do.
6. Discarding staged content after a failed apply.
7. Claiming “installed everywhere” after a single-profile apply.
8. Silent delete of pilot skills/memory when a system is removed — discuss retire.
9. Saving project narrative into user profile or operational memory.
10. Skipping preflight because the human is in a hurry — then shipping broken
    descriptions or duplicate creates.
11. Density-only edits of high-value lock lines without budget Q1–Q3.
12. Leaving recurring apply friction only in chat — patch the procedure skill.

## Verification checklist

- [ ] Inventory covered the intended sources; archives/backups ignored
- [ ] Sustainment filter applied (90-day / reuse / steer / lock / cross-project)
- [ ] Each keep-candidate has a destination layer
- [ ] Skill and/or memory preflight has no unaddressed FAIL
- [ ] Live-line shortens routed through `agent-memory-budget` Q1–Q3
- [ ] Recommended plan stated; human OK obtained before apply
- [ ] Applies succeeded before any staged discard
- [ ] On-disk / in-store state matches plan; queue matches hold/empty intent
- [ ] Multi-copy shared stores verified if applicable
- [ ] Rollout/distribute called out separately when global ship is intended

## Hermes adaptation

When installed on **Hermes Agent**, map the abstract terms as follows:

| This skill | Hermes |
|--|--|
| User profile | `USER.md` (always-on user block) |
| Operational memory | `MEMORY.md` |
| Skills | `SKILL.md` trees under the profile skills dir |
| Staged candidates | `pending/skills/`, `pending/memory/` when write approval is on |
| Project artifacts | Handoffs, ADRs, plans outside always-on memory |
| Local apply | Approve/apply helpers or `/skills` on surfaces that support it |
| Multi-copy identity | Shared MEMORY/USER across profiles — identity-copy before sync |

Hermes-oriented practice notes (optional; skip on non-Hermes hosts):

- Desktop may not expose `/skills` even when the CLI/TUI does — agent-assisted
  review of the pending directories remains valid.
- Description convention often used on multi-profile installs: trigger-first,
  short index line, HTML comment after frontmatter.
- Apply success on one `HERMES_HOME` does not by itself sync skills or memory to
  other profiles — treat distribute/sync/pin as a separate approved step.
- For compression bands, per-entry Q1–Q3, and raise criteria, load
  `agent-memory-budget`.
- Estate-private runbooks (named hosts, private scripts, Discord paths) stay out
  of this public skill; keep them in private ops skills if you have them.

**Not official Nous guidance** — community method developed while operating Hermes.
