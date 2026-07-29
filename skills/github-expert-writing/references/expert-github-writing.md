# Expert GitHub Writing Standards

Co-created by **ATtheGR8** & **Hermes Agent**. Copyright (c) 2026 Avery Thompson.

Canonical bar for **issue bodies, PR bodies, and PR/issue comments**.

**Not this skill:** `gh`/API lifecycle → bundled `github-issues` / `github-pr-workflow`; diff review mechanics → `github-code-review`; pre-commit gates → `requesting-code-review`.

Load this file whenever opening or rewriting public GitHub prose, or when posting
verification, correction, or response-to-review comments.

Worked example (**structure only**):
[NousResearch/hermes-agent#65982](https://github.com/NousResearch/hermes-agent/pull/65982) —
real PR plus verification / correction / author-reply thread.
**Inspired by that review quality.** Copy the **method**, not the product feature.

---

## Voice

- **Professional and personable** — a careful senior engineer talking to humans, not a changelog bot and not a hype reel.
- **Readable at every level** — lead with the plain-language point; then mechanism, files, SHAs, and jargon. Define uncommon terms once.
- **Direct** — problem and outcome in the first screen. No buried lede, no sycophancy, no "excited to share".
- **Fair** — separate "introduced here" vs "pre-existing"; say when a control experiment was bad; credit reviewers specifically for what helped.
- **Own errors fast** — corrections lead with what was wrong, show the proper control, narrow the claim; short apology, no groveling.

## Non-negotiables

1. **Problem / change first** — what, why, user-visible effect; `Fixes` / `Closes` / `Refs` when real.
2. **Mechanism** — step-by-step cause or fix path; cite paths, symbols, and commit SHAs that exist.
3. **Evidence** — setup, commands run, verbatim outputs (redacted), head SHA, versions when relevant.
4. **Tests when possible** — what ran, pass/fail counts, **baseline comparison** when claiming no regressions; **RED→GREEN** per fix when claiming a fix. **Never invent results.** If you could not run it, say blocked and why.
5. **Scope honesty** — this PR vs prior art; stacked bases / fork-diff caveats; deferred work and why.
6. **Actionable close** — concrete next steps; maintainer **options** when the call is policy/architecture, not a silent unilateral decision.
7. **Safety** — dummy credentials only (`<dummy>`, `sk-ant-…` shapes described not pasted); no tokens, private keys, customer data, or live secrets. Private triage links OK only if the public summary is self-contained.
8. **Depth scales with blast radius** — security, billing, data loss, production incidents → full verification genre. Normal features/fixes → full problem + fix + real test plan. Trivial docs/typos → short summary + how checked. Do not write a novel for a typo; do not ship a billing claim with "lgtm".

## Depth guide

| Risk / claim | Minimum bar |
|--------------|-------------|
| P0–P1 security, billing lane, data loss, prod incident | Full verification genre + fail-closed proofs + baseline |
| Behavioral feature / non-trivial bugfix | Problem, mechanism, fix, tests with real results, reviewer notes |
| Refactor / chore with behavior risk | Summary, risk, what was run, rollback note |
| Docs / typo / comment-only | 2–5 lines: what + how checked |

## Finding taxonomy (verification and review comments)

Label findings so skimming works:

- **F1, F2, …** — stable ids for the thread (do not renumber silently; add F5 rather than reshuffle).
- **Severity:** P0 (merge-blocker / unsafe), P1 (should block), P2 (important, fix soon), P3 (UX/nit), informational.
- **Area tag** optional: `(P2, billing)`, `(P3, UX)`.
- Each finding: **title → evidence → scope (this PR vs pre-existing) → concrete fix options**.

Reviewer severity icons from `github-code-review` remain valid on inline review:
Critical / Warning / Suggestion / Looks Good.

## Evidence checklist (copy into real writes)

- [ ] Head SHA or release under test
- [ ] Environment (OS, runtime, package/CLI versions) when behavior depends on it
- [ ] Isolation notes when relevant (`HERMES_HOME`, empty env, no ambient keys)
- [ ] Exact commands (copy-pasteable)
- [ ] Verbatim outputs (trim noise; keep proof lines)
- [ ] Dummy/redacted secrets only
- [ ] For "no regressions": failure set **identical to named baseline SHA**, or explain deltas
- [ ] For each fix claim: test name or repro that was RED, then GREEN
- [ ] Explicit "did not run X because Y" when blocked

## Genre index → templates (this skill)

Load with `skill_view(name='github-expert-writing', file_path='templates/…')`.

| Genre | Template |
|-------|----------|
| PR body — feature | `templates/pr-body-feature.md` |
| PR body — bugfix | `templates/pr-body-bugfix.md` |
| Issue — bug | `templates/bug-report.md` |
| Issue — feature | `templates/feature-request.md` |
| Issue — design / policy decision | `templates/design-decision.md` |
| Comment — independent verification | `templates/comment-verification.md` |
| Comment — correction / errata | `templates/comment-correction.md` |
| Comment — author response to review | `templates/comment-response-to-review.md` |

## Maintainer decision framing

When the change is policy-shaped (in-tree vs plugin, pin semantics, public API):

```markdown
## Open decision
1. **Option A** — … tradeoff …
2. **Option B** — … tradeoff …
3. **Park / follow-up** — …

Recommendation (non-binding): …
I will implement whichever you name; I will not restack unilaterally on a large reshape.
```

## Stacked / fork PR honesty

If GitHub cannot use the real base branch:

- State **stacked on #N** in the summary.
- Say the diff **includes base commits until #N lands**.
- Offer to restack to provider-only (or equivalent) the moment the base merges.
- Rebase notes: conflict count, what stayed byte-identical, new head SHA, gate vs new baseline.

## Anti-patterns

- Empty section shells left as `<!-- TODO -->` in a published body
- "Works on my machine" with no command/output
- Invented pass counts or CI green claims
- Pasting real API keys, cookies, or customer payloads
- Blaming "pre-existing" without a control on the correct provider/config
- Silent scope creep past review (slip large features into a "small fix" push without a comment)
- Hype / engagement bait / performative gratitude walls
- Renumbering findings so old replies point at the wrong item
- Asking maintainers to "LGTM" without stating residual risk

## Completion criteria (before you post)

- [ ] First screen answers: what is this, why, what should the reader do?
- [ ] Every factual claim is either evidenced or explicitly labeled assumption/blocked
- [ ] No secrets; dummies only
- [ ] Depth matches blast radius
- [ ] Open questions are options with owners (maintainer vs author), not vague "thoughts?"
- [ ] Links/SHAs resolve; issue keywords correct (`Fixes` only when this change truly fixes it)
