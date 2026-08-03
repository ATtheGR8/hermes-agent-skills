---
name: qa-vision
description: "Use when visual QA before human review of images/UI."
version: 1.0.0
author: ATtheGR8 & Hermes Agent
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [qa, vision, visual, verification, images, screenshots]
    related_skills:
      - dogfood
      - universal-agent-work-sop
---
<!-- skill: qa-vision — Visual QA: agent first-pass before human review. -->

# QA Vision (agent first-pass visual verification)

**Credits:** ATtheGR8 & Hermes Agent (co-created). Maintained by ATtheGR8.
Copyright (c) 2026 Avery Thompson. **Not** an official Nous Research / Hermes
product skill.

**Visual QA** = structured inspection of **pixels the user will judge** (images,
GIFs/stills, atlas/sprite rows, slides, screenshots, UI captures) **before**
inviting human review or promoting a candidate to “done/live.”

Complements — does not replace — domain skills (`dogfood` for web explore when
installed; pack/edit skills for sprite atlases; doc/slide skills for render
pipelines).

## When to use

- Any deliverable the user must **view/check/verify** visually
- Candidate vs baseline compares (sprites, comps, mockups, UI before/after)
- GIFs, sheets, PDFs/slides rendered to images, Desktop/app screenshots
- Before “promote,” “looks good?,” or “please check this”

**Don't use for:** pure code review; non-visual metrics-only green builds;
full exploratory web QA end-to-end (→ `dogfood` when installed); architecture
gates (→ work SOP / architect skills).

## Mandatory rule

**Agent first-pass before human review.**

1. Inspect with tools (`vision_analyze` and/or capture tools on stills).
2. Report concrete pass/fail + what you saw.
3. **Then** invite the human.

Never hand off “please check this” with no prior vision pass.
**Metrics-only is insufficient** (edge gap / fill / SSIM can pass while the
subject is chopped, ghosted, or doubled).

## Workflow

### 1. Scope

- What must look right (identity, layout, FX, text, single subject, …)
- Baseline to beat (prior version, reference frame, design)
- Promote bar (ship / candidate only / reject)

**Done when:** pass criteria are explicit enough to fail a bad candidate.

### 2. Prep evidence (don't vision a bad input)

| Step | Practice |
|------|----------|
| Prefer stills | Animated GIF → export key frames or strip as PNG/WebP/JPEG |
| Provider formats | If vision API rejects a type, convert (common: GIF → PNG) and retry |
| Absolute paths | Pass real filesystem paths the tool can read |
| Multi-scale | 1× full context + **4×** crop on the disputed region |
| Compare strip | Label panels: `baseline \| candidate \| prior` (or body \| cand \| vN) |
| Sample frames | For cycles/rows: at least **first and last played** (e.g. f0 and f7), not only the hero frame |
| Batch | Fan out several `vision_analyze` calls with **different questions** |

**Done when:** files exist on disk and match what the human will see.

### 3. Question craft

Prefer **pass/fail** and **BAD indices only** over open “describe the image.”
See `references/question-patterns.md`.

Good patterns:

- “Single subject only? List BAD frame indices only.”
- “Is the head/top edge complete vs baseline? Any crop or ghost?”
- “f0–f7: which fail identity / doubling / FX strength? BAD only.”
- “Compare left vs middle vs right: which panel is promote-ready?”

Bad patterns:

- “Describe this image.”
- “Does it look good?”
- One vague call covering 20 unstated criteria

**Done when:** each call can return a decision-usable answer.

### 4. Dual channel

| Channel | Role |
|---------|------|
| Metrics (fill, margins, histograms, diffs) | **Hints** — triage and regression signals |
| Vision (and human) | **Gate** — identity, completeness, ghosts, layout, text |

If metrics pass and vision fails → **fail**. Say so explicitly.

### 5. Report (before invite)

Use `templates/vision-qa-report.md` or equivalent:

1. **Verdict:** pass / fail / pass-with-residuals
2. **Evidence paths** (stills, strips)
3. **Per-check table** (criterion → result → note)
4. **Residuals** (what still wrong; blocking vs cosmetic)
5. **Promote:** ready / not ready / needs user taste call
6. **Next action** (one concrete step if fail)

**Done when:** a human can decide without re-doing the agent’s inspection from scratch.

### 6. Promote discipline

- Keep candidates off live/production paths until vision + user OK when the
  domain requires it (e.g. active asset vs `*-candidate.*`).
- Do not claim “fixed” after metrics-only re-pack.
- Re-vision after each material edit; don’t reuse an old pass.

## Tool map

| Need | Tool / path |
|------|-------------|
| Local image/GIF frame | Export still → `vision_analyze` |
| Browser page | `dogfood` / browser vision — still apply first-pass + report |
| Native app UI | Desktop/computer-use capture → same report bar |
| Slides/PDF/docs | Domain skill render-to-images → this skill’s questions/report |
| Sprite atlas / FX | Domain pack skill **plus** this first-pass/gate |

## Common failure modes (class-level)

| Failure | Symptom | Mitigation |
|---------|---------|------------|
| Metrics false pass | Gaps OK, subject incomplete | Vision on 4× + baseline compare |
| Single-frame hero bias | Mid frame pretty, ends broken | Always sample ends + mid |
| Ghost / double subject | Afterimage, second figure | Explicit “single subject?” + BAD indices |
| Format / tool reject | Vision 400 on GIF/odd type | Still PNG/JPEG; retry; don’t skip QA |
| Vague vision | Long description, no decision | Rewrite questions as pass/fail |
| Skip first-pass | “Please check” only | Block self; run workflow §1–5 |

## Common pitfalls

1. Inviting review with no agent vision pass
2. Treating fill/margin/SSIM as ship criteria
3. Visioning only one flattering frame
4. Unlabeled compare (no baseline)
5. “Looks fine” without residuals / promote call
6. Replacing web exploratory QA or domain pack skills with this umbrella

## Verification checklist

- [ ] Scope/pass bar stated
- [ ] Stills/strips on disk; formats vision-safe
- [ ] Multi-scale + baseline compare when a baseline exists
- [ ] Targeted vision calls (not one vague describe)
- [ ] Metrics used only as hints
- [ ] Report: verdict, residuals, promote-ready, evidence paths
- [ ] Human invited **after** agent pass
- [ ] Candidate not promoted on metrics-only

## Related

- Work discipline: `universal-agent-work-sop` (when installed)
- Web exploratory QA: `dogfood` (when installed)
