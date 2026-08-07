# interactive-decision-gates

Body-first **choice menus** for Hermes (and similar) agents: ranked options, fully determined option IDs, menu ≡ recommendation alignment, and discuss-then-apply locks.

## Credits

**ATtheGR8** & **Hermes Agent** — co-created.  
Maintained by [ATtheGR8](https://github.com/ATtheGR8).  
Copyright (c) 2026 Avery Thompson.

**Not** an official Nous Research / Hermes bundled skill.

## What you get

- `SKILL.md` — when to use, fully determined option IDs, ranking rules, menu alignment, surface-agnostic presentation, gate-walk, pitfalls

Pairs with `universal-agent-work-sop` and `it-architect` in this monorepo.

## Install

From this monorepo root:

```bash
cp -R skills/interactive-decision-gates ~/.hermes/skills/devops/interactive-decision-gates
```

Named profiles: use `~/.hermes/profiles/<name>/skills/devops/interactive-decision-gates` instead.

```text
skill_view(name='interactive-decision-gates')
```

## Scope

| In | Out |
|----|-----|
| Multi-option gates, ADR questions, install/apply menus | Silent execute after “looks good” |
| Fully determined option IDs | Nested maybe/optionally forks in one row |
| Body-first options on every surface | Chip/button-only option text |

## Companions (recommended, not required)

| Skill | Role if installed |
|---|---|
| `universal-agent-work-sop` | Re-load on apply of a mutating choice |
| `it-architect` | ADR/design package drafting after locks |

This skill is useful **alone** for body-first ranked menus.

## Version

Public **1.0.0** (first public release; fully determined IDs + menu≡rank; portable companions).

## Security

Documentation only. No secrets in menus or locks.

## License

MIT (see repository root [LICENSE](../../LICENSE)).
