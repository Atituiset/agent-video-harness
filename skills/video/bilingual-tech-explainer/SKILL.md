---
name: bilingual-tech-explainer
description: Turn a technical article, research notes, or docs into a bilingual (zh+en) explainer video for programmers. Narrative spine (wall → fix) + continuity kit (evolution rail / opening stage scaffolding / wall cards) + teaching-specific blueprint and evidence-card patterns. Depends on this repo's bilingual-video skill (the narration/captions/publishing general layer) and the official faceless-explainer workflow. Use when turning a technical article, research notes, or docs into a bilingual (zh+en) explainer video for programmers. 把技术文章/调研文档做成中英双语程序员科普视频。
---

# Bilingual tech explainer (article → zh+en explainer film)

**Dependencies**: this repo's `bilingual-video` skill (the bilingual production general layer: dual projects, narration & captions, iteration loop, publishing conventions, 26 pitfalls — read its `references/pitfalls.md` first) + the official `/faceless-explainer` workflow (`npx skills add heygen-com/hyperframes --skill faceless-explainer`). This skill defines only the explainer-specific narrative and visual layers.

Bundled assets (`<SKILL_DIR>` = this skill's directory):
- `recipes/agent-harness-explainer/` — frozen recipe (code-editorial design preset + BRIEF skeleton + storyboard skeleton), adoptable via the official `recipe.mjs use` or by copying `frame.md` manually
- `examples/reference-case-frame.html` — reference case-frame implementation (the thing to copy for structure / timing / rail / caption avoidance, see `examples/README.md`)

## Narrative spine: wall → fix

For tech-evolution / mechanism-teardown content, every layer must **hit a wall before the fix appears**: the previous layer's capability boundary is named first ("the model doesn't remember the previous turn — that's boundary #1"), then this layer's mechanism is introduced. When writing SCRIPT.md, self-check frame by frame: does this frame's opening answer "why is this being explained now"? Between cases there must be pivot sentences ("another path is…", "X cares about a different thing: …"), otherwise it's a rushed-slideshow video.

## The continuity kit (default for multi-frame explainers)

1. **Evolution rail**: a top progress rail (y≈48), in place at t=0 of every frame and static throughout. In hierarchy segments it shows layer nodes (past = solid, current = accent dot + label, future = hollow); in case segments it switches to journey dots + case dots. It is the visual anchor shared across the whole film — the main cure for the slideshow feel.
2. **Opening stage scaffolding**: by t≤0.45s every frame must already show kicker + full title + diagram skeleton (empty slots / base layers). The official injected 0.5s transition lands on the head of the next frame — without scaffolding, the audience repeatedly sees a blank canvas. VO-paced reveals are reserved for the detail layer only.
3. **Wall cards**: at each layer's opening, flash `✗ Boundary N · …`; when the mechanism lands, flip it to accent ✓ + strikethrough. This visualizes the narrative setup — the causal chain reads even on mute.

## Content patterns for explainers

- **Blueprint selection**: concept naming → `kinetic-type-beats`/`typewriter-reveal`; mechanism layers → `grid-card-assemble`/`comparison-split`/`agent-progress-theater`; cyclic flows → self-drawn ring + touring dot; cases/data → `dataviz-countup`; closing thesis → `kinetic-type-beats` relay + long hold.
- **Evidence cards**: benchmark screenshots / data figures from the source article are the most credible material for case frames (when the source is saved with a `_files/` directory, scan the images first — don't extract text only). Enter as a framed card + mono caption (source · date) after the numbers land.
- **Case series + overview**: parallel cases share one stage (kicker numbering + rail progress), swapping only the diagram content; close with a single positioning map / comparison table covering all objects ("same problem, different trade-offs"), then land the thesis.
- **Programmer aesthetics**: terminal/code surfaces may use dark panels + mono fonts; restrained accent color (at most one per frame); when there is no background music, mark it explicitly (`music: none`).
