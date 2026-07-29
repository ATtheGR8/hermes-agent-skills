# github-expert-writing

Evidence-first writing bar for **GitHub issues, pull requests, and substantial review comments** (verification, correction/errata, author response-to-review).

## Credits

**ATtheGR8** & **Hermes Agent** — co-created.  
Maintained by [ATtheGR8](https://github.com/ATtheGR8).  
Copyright (c) 2026 Avery Thompson.

**Not** an official Nous Research / Hermes bundled skill.

### Inspiration

Worked example (**structure only**): [NousResearch/hermes-agent#65982](https://github.com/NousResearch/hermes-agent/pull/65982) — real PR plus verification / correction / author-reply thread that inspired this bar. **Inspired by that review quality.** Copy the **method**, not the product feature.

## What you get

- `SKILL.md` — when to load, process, genre map  
- `references/expert-github-writing.md` — full standards (voice, evidence, depth scaling, anti-patterns)  
- `templates/` — PR bodies, issue bodies, verification / correction / response comments  

Pairs with stock Hermes lifecycle skills (`github-issues`, `github-pr-workflow`, `github-code-review`) for `gh`/API mechanics.

## Install

From this monorepo root:

```bash
cp -R skills/github-expert-writing ~/.hermes/skills/github/github-expert-writing
```

Then in Hermes:

```text
skill_view(name='github-expert-writing')
skill_view(name='github-expert-writing', file_path='references/expert-github-writing.md')
skill_view(name='github-expert-writing', file_path='templates/pr-body-feature.md')
```

## License

MIT (see repository root [LICENSE](../../LICENSE)).
