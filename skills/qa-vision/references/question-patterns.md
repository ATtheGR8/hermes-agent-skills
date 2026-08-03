# Vision question patterns

Use short, decision-shaped prompts. Prefer **BAD indices only** and
**pass/fail** over open description.

## Universal

- “Does this match the stated scope? Answer pass or fail; list defects only.”
- “Any blocking visual defect? List defects only; if none, say NONE.”
- “Promote-ready vs baseline? yes / no / user-taste — one sentence why.”

## Multi-frame strip / GIF stills

- “Frames left→right are f0…fn. Single subject only? List BAD indices only.”
- “Which frames have incomplete top/head/edge vs a complete subject? BAD only.”
- “Which frames show a ghost, double, or afterimage? BAD only.”
- “FX/motion present and coherent on which frames? List WEAK indices only.”

## Labeled compare strip (baseline | candidate | prior)

- “Three panels L→R: baseline, candidate, prior. Which is best for identity?”
- “Is candidate’s subject complete vs baseline? Crop, chop, or warp?”
- “Candidate vs prior: regression, improvement, or tie on [criterion]?”

## 4× detail crop

- “At this zoom: is the disputed edge complete? Any halo, seam, or ghost?”
- “Readable text? List wrong/missing characters only.”
- “Single clean silhouette? Any second figure or limb bleed?”

## UI screenshot / native capture

- “Layout broken? Overlap, cut-off, empty critical region — list only.”
- “Primary action visible and not obscured?”
- “Before vs after: intended change only, or collateral visual break?”

## Slide / PDF page image

- “Overflow, clipped text, or stacked elements? List only.”
- “Low-contrast text or icons that fail a quick read?”
- “Placeholder or lorem still visible? Quote it.”

## Anti-patterns

| Avoid | Prefer |
|-------|--------|
| “Describe this image.” | “Pass/fail on [criterion]; defects only.” |
| “Does it look good?” | “Promote-ready? yes/no + one why.” |
| One prompt for 15 criteria | Split calls; one decision class each |
| Vision only the hero frame | Ends + mid + 4× on failures |
