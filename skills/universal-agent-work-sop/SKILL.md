---
name: universal-agent-work-sop
description: "Use for all agent work: triage, plan, act, verify, sustain."
version: 1.2.1
author: ATtheGR8 & Hermes Agent
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [agent-work, sop, triage, planning, verification, sustainment]
    related_skills:
      - plan
      - spike
      - systematic-debugging
      - test-driven-development
      - requesting-code-review
      - subagent-driven-development
      - it-architect
      - architecture-adr
      - interactive-decision-gates
---
<!-- skill: universal-agent-work-sop — Universal work SOP (standard operating procedures): triage, act, verify, sustain. -->

# Universal Agent Work SOP (Standard Operating Procedures)

**Credits:** ATtheGR8 & Hermes Agent (co-created). Maintained by ATtheGR8. Copyright (c) 2026 Avery Thompson. **Not** an official Nous Research / Hermes product skill.

**SOP** means **standard operating procedures** — the repeatable work discipline in this skill (triage → gate → act → verify → sustain). After this definition, “SOP” refers to that discipline.

## Purpose

Apply this discipline to **all agent work**: research, planning, architecture, implementation, fixes, troubleshooting, testing, configuration, operations, documentation, data work, integrations, delegation, and sustainment.

The SOP (standard operating procedures) is always-on as a set of **principles**. The **full skill body is not sticky** after one load earlier in a conversation — see **Skill load and phase re-entry**. It is **not** permission to force a full proposal on every conversational turn. Scale visible ceremony to risk. The objective is to prevent avoidable rework, undisclosed assumptions, unsafe action, silent scope drift, and claims of completion without evidence.

## Scope and precedence

This skill is an umbrella work discipline. It does **not** replace specialist skills or durable artifacts.

Apply instructions in this order when they conflict:

1. Platform safety rules and direct user instructions.
2. Security, privacy, legal, and feasibility constraints. If safe completion is not feasible, stop and state why.
3. Repository-local instructions and accepted task-specific acceptance criteria.
4. Accepted ADRs, runbooks, and approved plans within their stated scope.
5. This SOP as the default work lifecycle.
6. Specialist skills for the selected work path.

Identity/tone files own persona. Project agent-rules and charter files own workspace-specific rules and goals. This SOP owns how an agent carries work from intent through verification and sustainment.

## Always-on principles

For every material claim, recommendation, or action:

1. **Investigate before asking.** Read readily available code, tests, configuration, manifests, documentation, skills, and runtime evidence before asking the user for information already discoverable without them.
2. **Make uncertainty visible.** Separate verified facts from assumptions and unknowns. Assumptions must be specific and falsifiable.
3. **Use risk-first proportionality.** Blast radius, reversibility, uncertainty, public/API impact, data sensitivity, privileges, production reach, and external side effects outrank line count.
4. **Preserve user control.** Do not silently broaden scope, redesign an approved solution, or perform a consequential external action without the required approval.
5. **Use the best available method.** Prefer an appropriate native UI, CLI, official documentation/API, skill, tool, script, or delegated worker; do not use a method merely because it is familiar.
6. **Verify before declaring completion.** Report actual checks and results. “Implemented” is not “complete” until agreed acceptance criteria are met or the remaining gap is explicitly accepted.
7. **Sustain what changes.** Consider the tests, documentation, runbooks, examples, ADRs, monitoring, ownership, rollback posture, and handoff state affected by durable work.

## Triage before action

Classify the task before deciding how much visible planning is needed.

| Class | Conditions | Required behavior |
|---|---|---|
| **Trivial** | Isolated, reversible, low-risk, one obvious correct form; no public/API, data, privilege, production, or external-effect change | Investigate what is cheap to verify; execute directly; report what changed and how it was checked. |
| **Standard** | Meaningful uncertainty, multiple plausible approaches, non-obvious cross-file effects, debugging, refactor, non-trivial documentation/data/config work, or a user-requested plan | Produce the concise work gate, obtain required approval, then execute and verify. |
| **High-blast** | Auth, credentials, money, deletion, migrations, data mutation, production config, external side effects, sensitive data, public API/schema, multi-node architecture, irreversible work, broad permissions, or high uncertainty | Produce the full work gate. Include safety/rollback/rollout evidence and trigger the relevant ADR, decision-gate, or domain procedure before action. |

If classification is uncertain, classify upward until evidence justifies a lower-risk path. A small diff is not proof of low risk.

## Skill load and phase re-entry

**Principles** in this skill are always-on once the agent is following the SOP. The **full skill body is not sticky**: a prior skill load (e.g. `skill_view` or host equivalent) earlier in the conversation does **not** count as loaded for a later phase.

### Actor-local load (MoA / multi-agent)

Skill load is **actor-local**: only the agent that will run tools/mutations counts. A planner, advisor, parallel MoA branch, or prior model turn that called `skill_view` does **not** satisfy load for the **executor**. Prefer “loaded **before the first substantive tool call or mutation** by this actor” over a fuzzy “same wall-clock turn” alone when roles are split.

### When to load or re-load this skill

Load (or re-load) this umbrella skill **before the first substantive tool call or mutation by this actor** when any of these hold:

1. **Phase change** — discuss / design / plan / gate → **execute / apply / mutate**
2. **Risk upgrade** — trivial → standard or high-blast; or blast radius grows mid-work
3. **New high-blast surface** — credentials, production or shared config, multi-system rollout, irreversible data/volume changes, external side effects
4. **Session start of material work** — standard/high-blast work when this skill has not been loaded on the **current turn**
5. **Handoff continuity** — user says `resume` / `resume <hint>` / `resume last` / park / write handoff (or pastes a handoff path): load **this skill with** the install’s **continuity/handoff skill when installed**. A handoff is **context, not authority** for live state and new mutations; **durable locks** in the file may still carry (do not re-open without cause). Not a prior skill load. Domain specialists load **in addition**.
6. **Durable decision artifacts** — author, revise, Accept, Reject, or multi-file design package work (ADR + plan + runbook + diagrams, architecture decision, options analysis): load **this skill**; also load `it-architect` **when installed** before the first mutation. Classify at least **standard**. Prefer the real architecture skill over any ADR **stub/redirect** name. If no architecture skill is installed, keep ADR work under this SOP’s standard/high-blast gates and any templates the user provides.
7. **Stub / redirect skills** — if the selected skill says “load X”, “absorbed into X”, or is only a redirect: load **this umbrella and the real target X** in the same turn. A stub load alone is **not** a completed specialist load.

### Umbrella and specialist together

- **Specialist skills do not replace this umbrella.**
- For standard/high-blast **apply**: load **this skill and** the relevant specialist **before the first mutating tool call** (same turn is fine; umbrella must not be omitted).
- Specialists own domain steps; this skill owns triage, gate, approval boundary, verification, and sustainment.
- **Redirects:** follow the target skill’s body; do not stop after reading the stub.

### Material entry registry (pair-load — not exhaustive)

| Entry | Load before first mutation |
|---|---|
| Handoff resume / park / write | this skill + continuity/handoff skill when installed (+ domain) |
| ADR / architecture decision / multi-file design package | this skill + `it-architect` **when installed** (not stub-only); else this skill + user/repo ADR templates |
| Host / multi-profile config or gateway apply | this skill + host-ops specialist when installed + domain specialist |
| Technical failure / regression fix | this skill + `systematic-debugging` before proposing the fix |

### Approval language

- A **conditional** choice (“Accept only after revise”, “after X then Y”) is **not** authority to perform the intermediate mutate unless that option’s text is a **fully determined apply/revise-now** action (see `interactive-decision-gates` when installed).
- Prefer separate option IDs: e.g. **R** = revise these artifacts now · **A** = Accept revised design · **H** = hold.

### Done when

- [ ] For standard/high-blast apply: this skill was loaded on the **apply turn** before the first mutating command
- [ ] Specialist (if any) loaded in addition, not instead — **real** target, not stub-only
- [ ] Prior “we loaded SOP at kickoff” was **not** used to skip re-entry after a phase change
- [ ] Handoff resume/park/write: this skill + continuity skill loaded on the **entry turn** before acting on the charter (**when** a continuity skill is installed)
- [ ] ADR/design mutate: this skill loaded on the **mutate turn**; `it-architect` also loaded **when installed**
- [ ] Conditional menu picks were not treated as revise/apply authority unless fully determined

## Investigate before asking

Before raising a blocking question or proposing action:

1. Read the relevant local instructions, source/configuration, tests, manifests, and nearby implementations.
2. Inspect the direct source of truth for live systems when available; do not treat old chat history as current state.
3. Check official documentation or official APIs before recommending unverified third-party alternatives.
4. Identify contradictions, missing evidence, and constraints that materially affect the outcome.
5. Ask only questions that cannot be answered safely through investigation and whose wrong answer would materially change the work.

**Done when:** each question is genuinely blocking or is intentionally deferred with a stated safe default.

## Concise work gate — standard work

Before starting a standard task, provide only the sections that materially apply:

1. **Goal and acceptance criteria** — restate the requested outcome and how success will be checked.
2. **Evidence and consequential unknowns** — important paths, commands, docs, or live facts inspected; clearly identify unverified facts that influence the plan.
3. **Blocking questions (0–3)** — only genuine blockers. Give each a recommended, fully determined default. If none exist, state zero.
4. **Material assumptions** — numbered, specific, falsifiable assumptions about data, failures, boundaries, state, environment, security/privacy/egress, scope, and testing as applicable.
5. **Plan** — artifacts to create/change, key interfaces or decisions, order of work, relevant alternative rejected in one clause, verification approach, and non-goals.
6. **Approval state** — state whether approval is needed before implementation or whether the user already expressly authorized direct execution.

Do not invent empty sections merely to fill a template.

**Done when:** the user can correct the outcome cheaply, choose a recommended default if needed, and understand what will change before consequential implementation starts.

## Full work gate — high-blast work

Use the concise gate plus the following:

1. **Risk and trust boundaries** — data classification, permissions, secrets, PII, network/egress, third parties, affected users/systems, and failure modes.
2. **Change safety** — backup, dry-run, staging, rollout, monitoring, rollback, recovery, or revocation strategy as applicable.
3. **Durable decision artifact** — ask whether an ADR is wanted for a new project or non-trivial technical decision; load `it-architect` **when installed** where its triggers apply.
4. **Explicit exclusions** — what is not being changed and what risk remains after the work.
5. **Decision gate** — present fully determined, ranked options when user choice is needed; load `interactive-decision-gates` **when installed** for the menu contract (otherwise keep full option text in the message body).

**Done when:** the proposed action, safety controls, rollback posture, owner decisions, and remaining risk are all visible before execution.

## Approval, changes, and implementation

- A direct, unambiguous instruction to execute is approval for the stated scope. Silence is not approval.
- **Approval authorizes scope; it does not waive skill load/re-entry or verification.** On design → execute, re-load this skill (and the specialist) before the first mutation.
- Partial approval authorizes only the accepted portion; keep other decisions open.
- Implement the approved plan. Do not silently change user-visible behavior, scope, risk, data handling, public interfaces, rollout, or acceptance criteria.
- If new evidence materially changes one of those things, stop, explain the changed fact and impact, recommend a revised path, and wait for the necessary decision.
- Internal implementation adjustments may proceed without a new gate only when they preserve the approved outcome and acceptance criteria, do not increase risk or scope, and are disclosed in the final report.

For long-running or multi-surface work, preserve the accepted gate and current status through the established handoff procedure. The continuity mechanism is owned by the install’s handoff/continue skills **when present**, not this skill.

## Select the specialist, do not duplicate it

Load **this umbrella and** the specialist for standard/high-blast **apply** — never the specialist alone as a substitute for this skill. This SOP chooses and sequences specialists; it does not copy their procedures.

| Work condition | Load / follow |
|---|---|
| User wants a plan only, with no execution | `plan` |
| A question needs a bounded, throwaway experiment | `spike` |
| Technical failure or regression | `systematic-debugging` before proposing a fix |
| New behavior, bug fix, or behavior-preserving refactor | `test-driven-development` where applicable |
| Architecture, multi-system, security, data, or durable technical decision | `it-architect` **when installed** (+ this umbrella; not an ADR stub alone) |
| User must choose among ranked paths | `interactive-decision-gates` when installed (+ this umbrella on apply of the chosen path) |
| Heavy implementation with separable tasks | `subagent-driven-development` and/or install delegation skills |
| Host / multi-profile estate operation | host-ops specialist when installed + domain skill |
| Pre-commit quality review | `requesting-code-review` |
| Cross-surface continuity | continuity/handoff skill when installed |

## Verification and final report

Every non-trivial task ends with a concise, evidence-backed report:

1. **Outcome** — what changed or was decided.
2. **Artifacts** — files, systems, or records affected.
3. **Verification** — commands, tests, inspections, UI checks, or runtime checks actually performed and their results.
4. **Acceptance status** — met, partially met, blocked, or explicitly deferred; never imply success when a check failed or was skipped.
5. **Safety action** — rollout, rollback, backup, recovery, or monitoring result when applicable.
6. **Sustainment** — docs, runbooks, examples, ADRs, tests, ownership, and handoff updates completed or deliberately deferred.
7. **Residual risk / next step** — only when material.

**Done when:** every agreed acceptance criterion is accounted for with evidence or an explicit exception accepted by the user.

## Sustainment and SOP maintenance

For durable changes, decide whether to update:

- tests and fixtures;
- user/developer documentation and examples;
- runbooks, monitoring, alerts, ownership, or support paths;
- ADRs, decision records, changelogs, and deprecation notes;
- handoffs and project status.

### Friction capture (after hard implement/debug)

When work was **non-trivial** (roughly 5+ tool calls, repeated failure modes, or a workaround that will recur):

1. Capture **symptom → mitigation** while it is fresh (short; no session narrative dump).
2. Write it into the **specialist** home (skill, estate script, runbook) — not this umbrella SOP and not MEMORY scrap.
3. Prefer **patch existing** specialist over a new near-skill.
4. Point only: write friction into the specialist that owns the surface (pending/apply, host ops, skill authoring) **when those skills are installed** — not into this umbrella.
5. **Done when:** a future agent can hit the same class of problem and find the fix without rereading chat.

Do **not** paste dated issue laundry lists into this SOP — they go stale and bloat always-on process.

Review this SOP after avoidable rework, a security or operational incident, repeated researchable questions, repeated mid-implementation stops, a material tool/workflow change, or a periodic quality review. Keep one source of truth; replace stale wording rather than accumulating competing rules.

Useful indicators, only when they inform improvement: avoidable rework, researchable questions asked, plan revisions before implementation, material mid-work stops, rollback events, and failed acceptance checks. Do not optimize for a metric at the cost of truthful delivery.

## Worked examples

### Example A — trivial, direct execution

**Request:** Correct an obvious spelling error in a README.

- Inspect the exact file and nearby style.
- Confirm it is documentation-only and has no generated-source or public-release complication.
- Make the correction directly.
- Report the file and the exact validation performed, such as markdown/link check if one exists.
- No full gate or approval wait is needed unless the user requested a plan-only workflow.

### Example B — standard work, concise gate

**Request:** Add a CLI flag that changes a default timeout.

- Inspect the command parser, configuration precedence, current tests, docs, and call sites.
- State the intended default, acceptance checks, and backward-compatibility assumption.
- Ask only if the desired default or override precedence is truly unknown; recommend a default.
- Plan parser/config/docs/tests and identify why a global hard-coded timeout is rejected.
- Wait for approval if direct execution was not already authorized.
- Implement, run the actual tests, and report behavior plus docs/tests updated.

### Example C — high-blast work

**Request:** Rotate a production integration credential and move it to a new permissions model.

- Treat as high-blast even if the diff is small.
- Identify secret custody, affected services, least-privilege scope, rollout window, revocation order, outage behavior, monitoring, and rollback/recovery.
- Create or update the appropriate ADR/runbook if the decision is durable.
- Obtain a fully determined user decision before rotation.
- Verify the new path, revoke the old path only after success criteria are met, and report evidence without exposing secrets.

### Example D — troubleshooting

**Request:** Fix an intermittent production error.

- Classify at least standard; high-blast if production data, access, or external side effects are involved.
- Load `systematic-debugging`; establish a tight repro or diagnostic loop before proposing a patch.
- Do not convert an observed symptom into a guessed root cause.
- Once root cause changes the approved plan or risk posture, use the proper gate before the fix.
- Verify the fix against the repro and report unresolved uncertainty honestly.

## Common pitfalls

1. **Full ceremony for every turn.** Principles are always on; visible gate depth is risk-scaled.
2. **Using line count as the risk classifier.** One permission or deletion change can be high-blast.
3. **Asking a question discoverable from the workspace.** Investigate first.
4. **Calling an assumption a verified fact.** Label uncertainty plainly.
5. **Presenting open-ended choices when a safe default exists.** Recommend a fully determined path.
6. **Treating approval for a plan as approval for an altered plan.** Re-gate material drift.
7. **Claiming done after editing without evidence.** Report actual checks and outcomes.
8. **Replacing specialist skills with generic SOP prose.** Select the specialist; do not duplicate it.
9. **Copying this full procedure into identity, USER, project agent-rules, or IDEA files.** Keep this skill as the full source of truth; other layers carry only short pointers or local constraints.
10. **Maintaining a second full copy.** If a lab IDEA/charter file pointed at this skill, keep it as a short pointer after adoption; project IDEA files remain project charters.
11. **Leaving implement friction only in chat.** Capture symptom→fix in the specialist skill/script; do not archive incident lists in this SOP.
12. **Dumping project/session issue logs into the umbrella SOP.** Wrong layer; use handoff or specialist sustainment instead.
13. **Treating an earlier skill load as still active after a phase change.** Design/discuss load does not cover execute/apply — re-load this skill.
14. **Specialist-only load on apply turns.** Config/ops/debug specialists do not replace umbrella triage/gate/verify; load both.
15. **Execute momentum skipping re-entry.** A clear “go/apply” is approval for scope — not a waiver of load/re-entry or verification.
16. **Handoff resume/park/write without this umbrella.** Continuity or domain skills alone are not enough — pair-load this skill; handoff files are context, not authority (locks may carry; live health does not).
17. **ADR/design mutate with stub-only or specialist-only load.** Loading an ADR stub alone (or any redirect) without this umbrella + the real architecture skill **when installed** is the same class of miss as handoff-without-umbrella.
18. **Treating a conditional menu option as revise/apply authority.** “Accept only after revise” is a gate order, not “revise now,” unless a separate fully determined option says so.
19. **Counting another MoA/planner/advisor skill load as this actor’s load.** Only the tool-executing agent’s load counts; re-load before first substantive tool/mutation.
20. **Treating Next #1 in a handoff as high-blast approval.** Resume starts at focus; still gate destructive/external apply.

## Verification checklist

- [ ] Task classified trivial, standard, or high-blast using risk rather than line count.
- [ ] Readily available evidence was inspected before asking questions.
- [ ] Verified facts, assumptions, and consequential unknowns are distinguished.
- [ ] Standard/high-blast work has an appropriate gate and required approval.
- [ ] Standard/high-blast apply: this skill re-loaded by the **executing actor** before first mutation (earlier session/MoA peer load does not count across phase change).
- [ ] Handoff resume/park/write: this skill + continuity skill loaded on the entry turn; handoff not treated as live authority (durable locks may carry).
- [ ] ADR/design mutate: this skill on the mutate turn; `it-architect` **when installed** (not stub-only).
- [ ] Relevant specialist skill was selected **in addition to** this umbrella when domain work needs it (not instead; real target if redirect).
- [ ] Material implementation drift was re-gated; safe internal adjustments were disclosed.
- [ ] Final report includes actual verification and acceptance status.
- [ ] Sustainment artifacts and residual risk were considered.
- [ ] Non-trivial friction captured in the specialist home (not only chat / not a SOP laundry list).
- [ ] No secrets, tokens, or private keys were placed in artifacts or reports.
