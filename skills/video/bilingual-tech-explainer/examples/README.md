# examples/

## reference-case-frame.html

A reference implementation of one case frame (the "Pi · minimal" frame from the production project) — the thing to copy when authoring new case frames. Covers:

- `<template>` fragment structure + `data-composition-id` + paused root-timeline registration
- Case-stage conventions: `✱ 案例 0N` kicker, top evolution rail (journey dots + case dots, current one highlighted in coral)
- Stage scaffolding erected within the opening 0.45s (empty slots + empty gauges), details revealed on narration word boundaries
- Seek-safe implementation of count-up + ring sweep (the count-up signature move)
- Entry timing and placement of evidence cards (real benchmark screenshots)

**Note**: this is a structural/motion reference, not a renderable composition. The `assets/figures/*.png` it references (real article benchmark screenshots) are not included in this repo — replace them with evidence images from your own article. The fonts under `assets/fonts/` are included (OFL licensed); the subsetting method is rule 19 in `references/pitfalls.md`.

案例帧参考实现（结构/动效抄写对象，非可直接渲染的合成）。详情见上方英文说明。
