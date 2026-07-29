---
name: github-expert-writing
description: "Use when writing GitHub issues, PRs, or review comments."
version: 1.0.0
author: ATtheGR8 & Hermes Agent
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [GitHub, Issues, Pull-Requests, Writing, Review, Verification]
    related_skills: [github-issues, github-pr-workflow, github-code-review, requesting-code-review]
---
<!-- skill: github-expert-writing — Expert evidence-backed GitHub issue/PR prose. -->

# GitHub expert writing

**ATtheGR8** & **Hermes Agent** — co-created. Maintained by ATtheGR8.
Copyright (c) 2026 Avery Thompson. Not an official Nous Research / Hermes product skill.

Worked example (**structure only**): [NousResearch/hermes-agent#65982](https://github.com/NousResearch/hermes-agent/pull/65982) —
real PR plus verification / correction / author-reply thread.
**Inspired by that review quality.** Copy the **method**, not the product feature.

Single package for **public GitHub prose**: issue bodies, PR bodies, and substantial
comments (verification, correction, response-to-review). Encodes an evidence-first bar:
problem first, mechanism, evidence, real tests, fair scope, human voice.


## When to use

Load **before drafting or posting**:

- New or rewritten **issue** (bug, feature, design/policy decision)
- New or rewritten **PR description**
- **Verification** write-up, **correction/errata**, or **author reply** to review findings
- Any GitHub comment where claims need commands, outputs, SHAs, or severity-tagged findings

**Do not use for:** `gh`/API lifecycle only (create branch, merge, labels) — keep
`github-issues` / `github-pr-workflow`. Inline diff review mechanics stay in
`github-code-review`. Local pre-commit gates stay in `requesting-code-review`.

## Required load sequence

1. `skill_view(name='github-expert-writing')` — this file
2. `skill_view(name='github-expert-writing', file_path='references/expert-github-writing.md')` — full bar
3. Matching template under `templates/` (see genre table in the reference)
4. Draft → self-check completion criteria in the reference → post via `gh`/API skills

## Non-negotiables (summary)

- Problem/change first; mechanism with real paths/SHAs
- Evidence: setup, commands, verbatim outputs (redacted); never invent test results
- Tests when possible; baseline when claiming no regressions; RED→GREEN per fix claim
- Depth ∝ blast radius (security/billing/prod → full verification genre; typo → short)
- Dummy secrets only; maintainer policy as numbered options, not silent unilateral calls
- Own mistakes with a correction comment (bad control → proper control → what still stands)

## Genre → template

| Genre | `file_path` |
|-------|-------------|
| PR feature | `templates/pr-body-feature.md` |
| PR bugfix | `templates/pr-body-bugfix.md` |
| Issue bug | `templates/bug-report.md` |
| Issue feature | `templates/feature-request.md` |
| Issue design decision | `templates/design-decision.md` |
| Verification comment | `templates/comment-verification.md` |
| Correction / errata | `templates/comment-correction.md` |
| Author response to review | `templates/comment-response-to-review.md` |

## Credits and maintenance

- **ATtheGR8** & **Hermes Agent** — co-created; maintained by ATtheGR8
- Copyright (c) 2026 Avery Thompson (repository LICENSE)
- Not an official Nous Research / Hermes bundled skill
- Prefer improving this skill tree in git rather than forking the bar into bundled `github-*` skills

## Completion before post

- [ ] First screen: what / why / what reader should do
- [ ] Claims evidenced or labeled blocked/assumption
- [ ] Template genre matched; depth matches risk
- [ ] No secrets; dummies only
- [ ] Issue keywords accurate (`Fixes` only when true)

## Common pitfalls

1. Writing the PR body from memory without loading this skill
2. Inventing pass counts or CI green
3. Pasting real tokens “just for the issue”
4. Full novel for a typo — or “lgtm” for a billing/security claim
5. Skipping evidence (commands/outputs) or inventing pass counts
