# agent-memory-budget

Manage finite **always-on agent memory**: measure pressure, inventory first,
compress without silent semantic loss, relocate runbooks into skills, and raise
limits only after explicit approval.

## Credits

**ATtheGR8** & **Hermes Agent** — co-created.  
Maintained by [ATtheGR8](https://github.com/ATtheGR8).  
Copyright (c) 2026 Avery Thompson.

**Not** an official Nous Research / Hermes bundled skill.

## What you get

- `SKILL.md` — pressure bands, non-limit fixes, mandatory per-entry Q1–Q3
  compress gate, raise criteria, multi-copy sync discipline, Hermes adaptation

Pairs with [`agent-knowledge-review`](../agent-knowledge-review/) for
keep/reject/destination on proposed skills and memory. Complements
[`universal-agent-work-sop`](../universal-agent-work-sop/) for general work
discipline.

## Install

From this monorepo root:

```bash
cp -R skills/agent-memory-budget ~/.hermes/skills/devops/agent-memory-budget
```

Named profiles use `~/.hermes/profiles/<name>/skills/` instead of `~/.hermes/skills/`.

Then in a **new** Hermes session:

```text
skill_view(name='agent-memory-budget')
```

### Optional compact USER pointer

```text
Memory budget: skill agent-memory-budget — inventory before raise; Q1–Q3 before compress.
```

## Scope

| In | Out |
|----|-----|
| Near-cap / over-limit always-on stores | Keep/reject of one-off project scrap (→ `agent-knowledge-review`) |
| Semantic compression and merge packs | Full multi-host private ops runbooks |
| Justified capacity increases | Blind shorter-wins sync policies |

## Method (one line)

Measure → band → non-limit fixes → Q1–Q3 pack → human OK → apply → verify copies.

## License

MIT (see repository root [LICENSE](../../LICENSE)).
