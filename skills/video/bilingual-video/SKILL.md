---
name: bilingual-video
description: The general layer for producing ANY bilingual (zh+en) video with HyperFrames, independent of video type — dual independent projects, edge-tts (Chinese) / Kokoro (English) narration with native word-boundary captions, the single-line re-record iteration loop, publishing conventions, and a 30-rule universal pitfalls checklist. Every route (explainer / promo / recut / motion-graphics …) passes through this layer first. Use when producing any bilingual (zh+en) video with HyperFrames, regardless of video type. 任何 HyperFrames 视频的中英双语生产通用层，与视频类型无关。
---

# Bilingual video production — the general layer (any video type)

This is the **shared foundation** for all bilingual video production, independent of video type. First route by intent via `/hyperframes` to a concrete workflow (faceless-explainer / product-launch-video / pr-to-video / talking-head-recut / embedded-captions / music-to-video / motion-graphics / general-video); this skill supplies the five things that stay invariant on top of all of them.

For technical explainer videos, use this repo's `bilingual-tech-explainer` directly (it depends on this skill).

## 1. Dual projects, never parameterized

Build two independent projects, `videos/<name>-zh` and `videos/<name>-en`. Narration length can differ by up to 15% between languages; independent timelines are the only way to avoid contortions. Order: **build zh end-to-end to render first; then the EN project copies zh's `compositions/frames/`, translates frame by frame, and re-times to English word boundaries** — reveals must re-anchor to the word actually being spoken; uniform rescaling is forbidden. Mirrored edits are done twice and verified twice.

## 2. Narration & captions (type-independent)

- **Chinese**: edge-tts `zh-CN-XiaoxiaoNeural --rate=+3%` (Kokoro's Chinese voices have an accent; its English voices are excellent). Use `scripts/gen-voice.py` — edge-tts's `boundary="WordBoundary"` native word boundaries directly produce an `audio_meta.json` compatible with the official pipeline, no Whisper needed:
  ```bash
  python3 -m venv scripts/.venv && scripts/.venv/bin/pip install edge-tts fonttools brotli
  scripts/.venv/bin/python <SKILL_DIR>/scripts/gen-voice.py --project .          # all lines
  scripts/.venv/bin/python <SKILL_DIR>/scripts/gen-voice.py --project . 3 4 5    # re-record only changed lines (merge)
  ```
- **English**: the official audio pipeline + Kokoro `af_sky` `--speed 1.05` (requires `pip install kokoro-onnx soundfile`, with `HYPERFRAMES_PYTHON` pointing at the venv).
- Both engines are deterministic. On both sides, use the official `audio.mjs sync-durations` to write durations back into the storyboard, and `captions.mjs` for captions.

## 3. The iteration loop (cheapest path for script edits)

Edit one line → re-record only that line (merge mode) → `sync-durations` → re-time only that frame (reveals re-anchor to the new word boundaries) → rebuild that frame's captions → `assemble-index` + `transitions inject` → `lint`/`check` → re-render. A single-line change costs minutes; never redo the whole film.

## 4. Delivery & publishing conventions

- Final check: ffmpeg-probe the closing moment of every frame plus several transition seams for visual inspection; file size is a quick health signal (a few-MB film with invisible remnants everywhere = broken timeline structure).
- Cover image: grab a highlight frame, `crop=1920:890` + `pad` back to 1080 to cut off the caption band.
- Bilibili: 科技→计算机技术 category, description with chapter timeline + asset credits, submit as original. YouTube: Chapters timeline, Science & Technology category, tick Altered content (synthetic voice disclosure).
- **A human must listen to the narration before publishing** (especially mixed zh/en words) — the model cannot hear it itself.

## 5. Pitfalls checklist (30 rules, all universal)

`<SKILL_DIR>/references/pitfalls.md`: five categories — narration/captions, composition/timeline, animation/seek-safety, text/contrast, workflow/collaboration. Read it before dispatching tasks to any agent (or doing it yourself).
