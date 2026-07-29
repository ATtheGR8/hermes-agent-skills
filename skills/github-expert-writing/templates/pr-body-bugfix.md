## Summary

<!-- One screen: what broke, who hit it, what this PR changes. Fixes #N when true. -->

Fixes #

## Bug

### Symptom

<!-- What users/operators observed. Include timing/environment if relevant. -->

### Impact

<!-- Severity: incorrect answers, billing, data loss, hang, security, etc. -->

## Root cause

<!-- Step-by-step. Cite paths/symbols. Separate trigger from underlying mechanism. -->

1. …
2. …
3. Therefore: …

## Fix

<!-- What changed and why this closes the hole. Call out adjacent holes closed in the same pass. -->

- …
- …

## How to verify

<!-- Reviewer-reproducible. Dummy credentials only. -->

**Repro (pre-fix / still on main if unfixed)**

```text
# commands
```

**Expected after fix**

```text
# commands + proof lines
```

## Test plan

- Regression tests: <!-- file::test names; each proven RED on pre-fix when possible -->
- Broader suite: <!-- command + result vs baseline `<sha>` -->
- Manual / prod signal: <!-- optional; no secrets -->

- [ ] Regression test added (or justified why not)
- [ ] Suite green or baseline-equal failures only
- [ ] Manual repro confirms fix (or N/A: reason)

## Risk assessment

**Low / Medium / High** — <!-- blast radius, who else shares the code path, rollback -->

## Residuals / follow-ups

<!-- Honest leftovers; do not hide known escapes. -->
