## Independent hands-on verification (<!-- env: OS / role -->)

Short version: **<!-- core claim holds / holds with residuals / does not hold -->.**
Findings **F1…** below. Depth matches blast radius; see skill writing standards.

**Setup**

- PR / commit under test: `<!-- sha or refs/pull/N/head -->`
- OS / runtime / package versions: …
- Isolation: <!-- e.g. fresh HERMES_HOME, empty .env, which auth path — no secrets -->
- Config (redacted):

```yaml
# only non-secret keys that matter
```

---

## Confirmed working

1. **<!-- claim -->**

```text
$ <!-- exact command -->
<!-- verbatim output (trim noise; keep proof) -->
```

2. **<!-- e.g. fail-closed / billing / resume -->**

```text
$ …
```

---

## F1 (P<!--0-3-->, <!-- area -->) — <!-- title -->

**Evidence**

```text
$ …
```

**Scope** — <!-- introduced in this PR / pre-existing / unclear — with control if you claim pre-existing -->

**Fix options**

1. …
2. …
3. Document-only / defer — …

## F2 (P…, …) — …

<!-- repeat -->

---

## Verdict

- **Merge blockers:** F…
- **Should fix soon:** F…
- **Nits / informational:** F…
- Happy to re-run against a new head (`<!-- offer -->`).

<sub><!-- Optional: tools used; every command above was executed; outputs verbatim. --></sub>
