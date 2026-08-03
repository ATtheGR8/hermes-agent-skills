# agent-knowledge-review

Decide whether proposed or existing **agent skills, user-profile lines, and
operational memory** deserve durable retention — and if so, **where** and **in
what shape**.

## Credits

**ATtheGR8** & **Hermes Agent** — co-created.  
Maintained by [ATtheGR8](https://github.com/ATtheGR8).  
Copyright (c) 2026 Avery Thompson.

**Not** an official Nous Research / Hermes bundled skill.

## What you get

- `SKILL.md` — destination map, 90-day sustainment filter, inventory → classify →
  preflight → recommend → apply → verify, synthetic examples, Hermes adaptation

Pairs with [`agent-memory-budget`](../agent-memory-budget/) for capacity,
compression, and limit raises. Complements
[`universal-agent-work-sop`](../universal-agent-work-sop/) for general work
discipline.

## Install

From this monorepo root:

```bash
cp -R skills/agent-knowledge-review ~/.hermes/skills/devops/agent-knowledge-review
```

Named profiles use `~/.hermes/profiles/<name>/skills/` instead of `~/.hermes/skills/`.

Then in a **new** Hermes session:

```text
skill_view(name='agent-knowledge-review')
```

### Optional compact USER pointer

```text
Knowledge review: skill agent-knowledge-review — 90-day filter; reject is success; skills≠memory dumps.
```

## Scope

| In | Out |
|----|-----|
| Keep / reject / redirect durable agent knowledge | Pure char-limit compress packs (→ `agent-memory-budget`) |
| Staged queues **or** manual audits | Project handoff narrative as always-on memory |
| Skills + user profile + operational memory | Framework-private host runbooks (keep those private) |

## Method (one line)

Inventory → classify destination → preflight → recommend → human OK → apply → verify.

## License

MIT (see repository root [LICENSE](../../LICENSE)).
