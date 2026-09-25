# Pitfalls checklist (self-contained)

All rules distilled from one full production run (long technical article → bilingual 17-frame explainer video, five rework rounds). Have any agent read this file before dispatching tasks to it.

## Narration & captions

1. Chinese TTS: edge-tts `zh-CN-XiaoxiaoNeural --rate=+3%`. Kokoro's Chinese voices have an accent, but its English voice (af_sky 1.05x) is excellent.
2. edge-tts's `Communicate(..., boundary="WordBoundary")` provides native word boundaries (the default is SentenceBoundary — you must pass it explicitly). It can directly generate an `audio_meta.json` compatible with the official pipeline (shape: `{bgm, voices:[{frame, path, duration_s, words:[{id,text,start,end}]}], sfx}`) — more accurate and cheaper than Whisper alignment.
3. SCRIPT.md frame headings must use half-width `(Frame N)` — full-width `（Frame N）` is not matched by the parser and silently generates 0 narration lines.
4. Kokoro/edge-tts output is deterministic: for script edits, re-record only the changed lines and merge them into audio_meta.json; untouched frames need no work at all.
5. Duration estimation: ~4.5 chars/second for Chinese is optimistic; dense technical explainers overrun by 10–16%. Remember to sync the storyboard's duration values.

## Composition & timeline

6. DOM ids/classes starting with a digit (`01-hook-bg`) make querySelectorAll throw SyntaxError and kill the whole frame's script — they must start with a letter. The lint warning `id_requires_css_escape` is the omen.
7. Every full-length clip owns its own `data-track-index` lane; overlaps within one lane are rejected by the assembler.
8. Nested GSAP timelines are not scrubbed by the capture engine — to shift a timeline as a whole, mechanically shift all tweens with a script instead of nesting.
9. When renumbering frames / reordering the storyboard, heading replacement must use exact full-heading matches (a partial regex first matches a newly inserted same-prefix frame block, misaligning entire caption segments). After edits, reconcile frame# × duration × src.
10. Absolutely-positioned decorative elements belong directly under `#root`; inside a child container with `position:absolute` they are positioned relative to it and fly off-canvas.

## Animation & seek safety

11. Don't animate SVG arcs with GSAP `attr: stroke-dashoffset` — a same-named CSS declaration overrides it, leaving only the endpoints (the "broken arrow"). Tween the CSS property `strokeDashoffset` instead.
12. Arrow's three laws: tip stops ≥14px from the target; use an explicit polygon triangle placed after the node in DOM order (later paints on top); verify direction against the path tangent. Don't use SVG `marker-end` (refX semantics are a pit).
13. A touring highlight dot's parking positions must avoid all arrows.
14. Elements "flying into a container" should dock at the container's edge with a visible gap; flying to the center and fading out makes hold frames read as "the stage is empty".
15. `tl.set(el, {innerText})` is not seek-safe — flip state with stacked dual elements + autoAlpha crossfade.
16. GSAP's onUpdate orbit computations are skipped under `seek()` (suppressEvents) — do orbit-type motion with seekable transform tweens (e.g. rotating a parent `<g>`).

## Text & contrast

17. All text uses solid colors at ≥4.5:1 contrast — `check` samples animation mid-states, and low-opacity decorative text will always blow up the WCAG audit.
18. `mask-image` fade-outs turn scrolling text into ghost text whose contrast mathematically cannot pass (1:1), and no color change saves it — hard-cut outbound elements with `tl.set(opacity: 0)` at the moment they cross the boundary; lines that must remain visible use a solid dimmed color (e.g. rgb(129,128,126)).
19. CJK fonts: never put a font name that doesn't exist on the machine into a font stack; subset with `pyftsubset --text-file=<project glyphs> --flavor=woff2` (16MB → ~112KB) into `assets/fonts/` and reference via `@font-face`.

## Workflow & collaboration

20. System Python is protected by PEP 668 → build a venv inside the project (`scripts/.venv`). Kokoro needs `kokoro-onnx + soundfile` + `HYPERFRAMES_PYTHON` pointing at the venv.
21. Extracting only the body text of a saved web page loses all images — scan the `_files/` directory first; real benchmark screenshots / data figures are the best "evidence cards" for case frames.
22. The transition lands on the first 0.5s of the next frame — every frame must erect its stage scaffolding (kicker + title + diagram skeleton) by t≤0.45s, otherwise the audience repeatedly sees a blank canvas.
23. Cross-frame continuity comes from a persistent element shared across the whole film (the top evolution rail), not from transitions.
24. Large parallel sub-agent fan-out (>10) easily hits usage limits; if hit, recover with resume. Sub-agents' temporary verification files are deleted right after use (loose html files in the project root trigger multiple_root_compositions).
25. Parallel sub-agents overwrite each other's shared `snapshots/` directory — copy verification frames to a private path immediately after capture.
26. The model cannot hear the narration itself — a human must listen before publishing (especially mixed zh/en words). If unsatisfied, re-record by line + re-time the single frame; the cost is minutes.
