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
| [universal-agent-work-sop](skills/universal-agent-work-sop/) | Work SOP (standard operating procedures) **1.2.7**: triage, plan, act, verify, sustain |
| [interactive-decision-gates](skills/interactive-decision-gates/) | Body-first choice menus: fully determined option IDs, ranked gates |
| [qa-vision](skills/qa-vision/) | Agent first-pass visual QA before human review of images/UI |
| [agent-knowledge-review](skills/agent-knowledge-review/) | Review agent skills/memory for durable retention (90-day filter) |
| [agent-memory-budget](skills/agent-memory-budget/) | Always-on memory pressure: inventory, compress (Q1–Q3), or raise |

## Install (primary)

Clone this repo, then copy the skill you want into your Hermes skills directory:

```bash
git clone https://github.com/ATtheGR8/hermes-agent-skills.git
cd hermes-agent-skills

# GitHub issue/PR prose
cp -R skills/github-expert-writing ~/.hermes/skills/github/github-expert-writing

# IT solutions architecture (ADRs / plans / reviews)
cp -R skills/it-architect ~/.hermes/skills/devops/it-architect

# Work SOP = standard operating procedures (triage / gates / verify)
cp -R skills/universal-agent-work-sop ~/.hermes/skills/devops/universal-agent-work-sop

# Choice menus / decision gates
cp -R skills/interactive-decision-gates ~/.hermes/skills/devops/interactive-decision-gates

# Agent first-pass visual QA
cp -R skills/qa-vision ~/.hermes/skills/software-development/qa-vision

# Durable knowledge keep/reject/destination review
cp -R skills/agent-knowledge-review ~/.hermes/skills/devops/agent-knowledge-review

# Always-on memory budget / compress vs raise
cp -R skills/agent-memory-budget ~/.hermes/skills/devops/agent-memory-budget
```

Named profiles use `~/.hermes/profiles/<name>/skills/` instead of `~/.hermes/skills/`.

Restart or start a new Hermes session so the skill index picks it up. Load with:

```text
skill_view(name='github-expert-writing')
skill_view(name='universal-agent-work-sop')
skill_view(name='it-architect')
skill_view(name='interactive-decision-gates')
skill_view(name='qa-vision')
skill_view(name='agent-knowledge-review')
skill_view(name='agent-memory-budget')
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
