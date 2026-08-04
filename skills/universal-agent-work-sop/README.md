# universal-agent-work-sop

Umbrella **work SOP (standard operating procedures)** for Hermes (and similar) agents: triage by risk, investigate before asking, gate non-trivial work, verify before “done,” and sustain what changed.

**SOP** = **standard operating procedures** (the repeatable work discipline in `SKILL.md`).

## Credits

**ATtheGR8** & **Hermes Agent** — co-created.  
Maintained by [ATtheGR8](https://github.com/ATtheGR8).  
Copyright (c) 2026 Avery Thompson.

**Not** an official Nous Research / Hermes bundled skill.

## What you get

- `SKILL.md` — full standard operating procedures: always-on principles, **skill load / phase re-entry**, trivial/standard/high-blast triage, concise and full work gates, specialist routing, verification report, pitfalls

Pairs well with skills in this monorepo (`it-architect`, `github-expert-writing`) and common Hermes skills (`plan`, `systematic-debugging`, `test-driven-development`, etc.) when those are installed.

## Install

From this monorepo root:

```bash
cp -R skills/universal-agent-work-sop ~/.hermes/skills/devops/universal-agent-work-sop
```

Named profiles: use `~/.hermes/profiles/<name>/skills/devops/universal-agent-work-sop` instead.

Then in Hermes:

```text
skill_view(name='universal-agent-work-sop')
```

### Optional always-on pointer

Hermes does not auto-run every skill every turn. To nudge the agent, add a short line to your user profile / house rules, for example:

```text
Work SOP: skill universal-agent-work-sop — for all agent work, load skill first; re-load on design→execute; triage trivial/standard/high-blast; investigate before ask; gate non-trivial; verify before done.
```

Keep the full procedure in the skill — do not paste the whole SOP (standard operating procedures) into USER/SOUL/AGENTS.

## Scope

| In | Out |
| ---- | ----- |
| How to carry any material agent task | Specialist deep procedures (debug, TDD, ADR prose) |
| Risk-scaled gates and verification | Replacing security platform rules |
| Choosing which specialist to load | Your private multi-profile estate ops |

## Security

Documentation only. No API keys required. Do not put secrets into gates, reports, or commits.
