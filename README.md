# hermes-agent-skills

Public collection of **[Hermes Agent](https://github.com/NousResearch/hermes-agent)** skills maintained by **[ATtheGR8](https://github.com/ATtheGR8)**.

Each skill lives under `skills/<skill-name>/` and follows the usual Hermes layout (`SKILL.md`, optional `references/`, `templates/`, etc.).

## Credits

**ATtheGR8** & **Hermes Agent** — co-created.  
Maintained by [ATtheGR8](https://github.com/ATtheGR8).  
Copyright (c) 2026 Avery Thompson (see [LICENSE](LICENSE)).

This is **not** an official Nous Research / Hermes product skill pack unless a skill’s README says otherwise.

## Skills

| Skill | Description |
|-------|-------------|
| [github-expert-writing](skills/github-expert-writing/) | Evidence-first GitHub issues, PRs, and review comments |
| [it-architect](skills/it-architect/) | IT solutions architecture: ADRs, options, plans, reviews (+ EA-lite) |

## Install (primary)

Clone this repo, then copy the skill you want into your Hermes skills directory:

```bash
git clone https://github.com/ATtheGR8/hermes-agent-skills.git
cd hermes-agent-skills

# GitHub issue/PR prose
cp -R skills/github-expert-writing ~/.hermes/skills/github/github-expert-writing

# IT solutions architecture (ADRs / plans / reviews)
cp -R skills/it-architect ~/.hermes/skills/devops/it-architect
```

Named profiles use `~/.hermes/profiles/<name>/skills/` instead of `~/.hermes/skills/`.

Restart or start a new Hermes session so the skill index picks it up. Load with:

```text
skill_view(name='github-expert-writing')
```

### Zip download

GitHub → **Code** → **Download ZIP** → unpack → copy `skills/<name>/` the same way.

## Optional: Hermes taps (future)

If you use `hermes skills tap` against multi-skill GitHub repos, you may be able to add this repository as a source and install by skill name. **Layouts and CLI flags vary by Hermes version** — treat tap install as optional. The **clone + copy** path above is the supported baseline.

```bash
# Example only — verify against your `hermes skills tap --help` before relying on it
# hermes skills tap add ATtheGR8/hermes-agent-skills
# hermes skills install github-expert-writing
```

## Security

- Skills in this repo are **documentation and templates** (no API keys required to use).
- Do not paste real tokens, private keys, or customer data into issues/PRs — the writing bar forbids it.
- Review any skill before installing, as you would any third-party agent skill.

## License

MIT — [LICENSE](LICENSE).
