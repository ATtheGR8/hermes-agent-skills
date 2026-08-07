# it-architect

**Solutions Architect** practice for IT / technical systems: evidence-first ADRs, options analyses,
implementation plans, architecture reviews, and decision gates — with optional **EA-lite**
(capability maps / light views) when estate-level framing helps.

## Credits

**ATtheGR8** & **Hermes Agent** — co-created.  
Maintained by [ATtheGR8](https://github.com/ATtheGR8).  
Copyright (c) 2026 Avery Thompson.

**Not** an official Nous Research / Hermes bundled skill.

## What you get

- `SKILL.md` — when to load, **pair-load with work SOP**, process, genre map, decision propagation  
- `references/architect-writing.md` — full SA writing bar  
- `references/ea-lite.md` — optional thin EA vocabulary (not TOGAF)  
- `templates/` — ADR (concise + heavy), options, plan, review, gates, capability map  

**ADR diagrams (required by this bar):** every ADR ships **both** a markdown flowchart (Mermaid preferred) and a **diagrams.net / draw.io** `.drawio` file, plus object and edge legends so labels are explicit and visible. Prose decisions remain source of truth.

Pairs with this monorepo’s `universal-agent-work-sop` and `interactive-decision-gates`, stock Hermes `architecture-diagram`, and optional `github-expert-writing`.

## Install

From this monorepo root:

```bash
cp -R skills/it-architect ~/.hermes/skills/devops/it-architect
# recommended companion
cp -R skills/universal-agent-work-sop ~/.hermes/skills/devops/universal-agent-work-sop
```

Named profiles: use `~/.hermes/profiles/<name>/skills/devops/…` instead.

Then in Hermes:

```text
skill_view(name='universal-agent-work-sop')
skill_view(name='it-architect')
skill_view(name='it-architect', file_path='references/architect-writing.md')
skill_view(name='it-architect', file_path='templates/adr.md')
```

## Scope

| In | Out |
|----|-----|
| IT/systems solutions architecture | Pure code feature blueprints |
| ADRs, plans, design reviews | Full enterprise TOGAF delivery |
| Required dual ADR diagrams (Mermaid + draw.io) | Official Nous product claims |
| Optional EA-lite framing | Install-private multi-profile sync internals |

## Companions (recommended, not required)

| Skill | Role if installed |
|---|---|
| `universal-agent-work-sop` | Umbrella pair-load before mutate |
| `interactive-decision-gates` | Accept/Revise/Hold menus with fully determined IDs |
| `architecture-diagram` / draw.io tooling | Diagram production aids (prose still requires Mermaid + `.drawio` artifacts) |

This skill is useful **alone** for ADR shape and templates.

## Version

Public **1.2.0** (umbrella pair-load + decision propagation).

## Security

- Documentation and templates only — no API keys required.
- Do not paste tokens, private keys, customer data, or private host inventory into ADRs.
- Review before install, as with any third-party agent skill.

## License

MIT (see repository root [LICENSE](../../LICENSE)).
