# qa-vision

Agent **first-pass visual QA** before human review of images, GIFs/stills,
sprite/atlas rows, slides, screenshots, and UI captures.

## Credits

**ATtheGR8** & **Hermes Agent** — co-created.  
Maintained by [ATtheGR8](https://github.com/ATtheGR8).  
Copyright (c) 2026 Avery Thompson.

**Not** an official Nous Research / Hermes bundled skill.

## What you get

- `SKILL.md` — when to load, mandatory first-pass, workflow, dual channel (metrics=hints, vision=gate)
- `templates/vision-qa-report.md` — report shape before inviting review
- `references/question-patterns.md` — pass/fail question bank

Pairs with stock Hermes `vision_analyze` (and browser/desktop capture tools when available). Complements `dogfood` for exploratory web QA; does not replace domain pack/render skills.

## Install

From this monorepo root:

```bash
cp -R skills/qa-vision ~/.hermes/skills/software-development/qa-vision
```

Named profiles use `~/.hermes/profiles/<name>/skills/` instead of `~/.hermes/skills/`.

Then in a **new** Hermes session:

```text
skill_view(name='qa-vision')
```

### Optional compact USER pointer

```text
Visual QA: skill qa-vision — agent first-pass before human review; metrics≠gate.
```

## License

MIT (see repository root [LICENSE](../../LICENSE)).
