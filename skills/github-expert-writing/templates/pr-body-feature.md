## Summary

<!-- 2–4 sentences a busy maintainer can trust. What lands, why, user-visible effect. -->

<!-- Link issues: Closes #N / Fixes #N / Refs #N -->

<!-- If stacked: **Stacked on #N** — merge that first; until then this diff includes its commits. -->

## Problem / Motivation

<!-- Who hurts today? What is broken or missing? Keep plain language first. -->

## What's in this head

<!-- Group by theme, not by file dump. Include short SHAs when helpful. -->

- **Core** (`sha…`): …
- **Hardening / follow-ons** (`sha…`): …

## How it works

<!-- Step-by-step mechanism. Cite paths/symbols. Diagram only if it earns its keep. -->

1. …
2. …
3. …

## Configuration / compatibility

<!-- Defaults, flags, migrations, fail-closed posture, what stays unchanged when unset. -->

## Test plan

<!-- Real commands and results. Never invent. Depth ∝ blast radius (see references/expert-github-writing.md). -->

**Automated**

```text
# commands run
```

- Result: <!-- e.g. N passed; failing set identical to baseline `<sha>` (K known env failures, none introduced) -->
- New/regression tests: <!-- names; note RED→GREEN if fixing a bug -->

**Manual** (when behavior is user-visible or security/billing-sensitive)

1. Setup: <!-- OS, versions, isolated env, auth path — no secrets -->
2. Steps + expected: …
3. Observed: <!-- verbatim proof lines -->

- [ ] Unit / integration tests pass (or baseline-equal failures explained)
- [ ] Manual path above exercised (or N/A: reason)
- [ ] No secrets in diff or body

## Risks and residuals

<!-- Blast radius, known gaps, deliberate non-goals, rollback. -->

## Notes for reviewers

<!-- Where to start, open maintainer decisions (numbered options), CI-less fork caveat if any. -->

## Open maintainer decisions (if any)

1. **Option A** — …
2. **Option B** — …
3. **Defer** — …

Recommendation (non-binding): …
