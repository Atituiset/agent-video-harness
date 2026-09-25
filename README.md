# skills

**[中文文档](README.zh-CN.md)** · English

My personal agent-skills collection. Install any skill with the skills CLI: `npx skills add Atituiset/skills --skill <name>`.

## Skills

### bilingual-tech-explainer

An open-source workflow that turns technical articles into **bilingual (zh+en) explainer videos for programmers**.

An open-source workflow that turns technical articles into **bilingual (zh+en) explainer videos for programmers**. Built on [HyperFrames](https://hyperframes.heygen.com) (HTML-as-video) + edge-tts/Kokoro narration + native word-boundary captions. The entire pipeline is drivable by any coding agent (Kimi Code / Claude Code / OpenCode / Codex …).

Proven in production: *"From One LLM Call to a Full Harness"* — a 17-frame bilingual explainer (zh 3m33s / en 3m10s) covering the LLM → context → ReAct → tool-calling → memory → Harness evolution, eight real harnesses (Pi / OpenCode / Codex / Hermes / Claude Code / DeepSeek Harness / Grok Build / Kimi Code), and a nine-way positioning map.

## Features

- **Independent bilingual projects** — zh/en timelines stay separate; Chinese narration via edge-tts (Xiaoxiao), English via Kokoro (af_sky); captions aligned from native TTS word boundaries, no Whisper needed
- **Continuity toolkit** — a persistent evolution rail, stage scaffolding within the first 0.45s of every frame, and a "wall card" motif; cures the rushed-slideshow feel
- **Narrative spine** — wall → fix: every engineering layer appears *for a reason*
- **26 hard-won rules** — arrow geometry, CJK font subsetting, WCAG ghost text, seek-safety, and more (`references/pitfalls.md`)
- **Agent-agnostic** — the skill is plain Markdown + CLI scripts; any agent that can run a shell can drive it (verified with Kimi Code and OpenCode)

## Install

Prerequisite: the `npx hyperframes` CLI (see HyperFrames docs).

```bash
# via the skills CLI (recommended)
npx skills add Atituiset/skills --skill bilingual-tech-explainer

# or copy manually
cp -r skills/bilingual-tech-explainer ~/.agents/skills/          # Kimi Code / generic
cp -r skills/bilingual-tech-explainer ~/.claude/skills/          # Claude Code
cp -r skills/bilingual-tech-explainer ~/.config/opencode/skills/ # OpenCode
```

Also make sure the official workflow is installed: `npx skills add heygen-com/hyperframes --skill faceless-explainer`.

## Usage

Tell your agent:

> Read the bilingual-tech-explainer skill and turn this article (path/URL) into a bilingual explainer video for Bilibili and YouTube. Working directory: videos/<project>.

The agent runs the official faceless-explainer pipeline (scaffold → design preset → storyboard & script → narration → per-frame builders → assembly → checks → render); the skill supplies the delta layer.

The skill directory is fully self-contained and installs with everything it needs:

| Path | What it is |
|---|---|
| `scripts/gen-voice.py` | edge-tts narration with native word boundaries → `audio_meta.json` |
| `recipes/agent-harness-explainer/` | Frozen recipe: code-editorial design preset + storyboard skeleton |
| `examples/reference-case-frame.html` | Reference case-frame implementation (see `examples/README.md`) |
| `references/pitfalls.md` | 26 production-tested rules — have any agent read this first |

## Project layout convention

```
videos/<name>-zh/   # Chinese project (build first, full pipeline)
videos/<name>-en/   # English project (copy zh frames → translate → re-time to word boundaries)
```

## License

MIT (see LICENSE). Third-party font files under `examples/assets/fonts/` keep their original licenses (EB Garamond / Inter / JetBrains Mono / Noto Sans SC — all OFL).
