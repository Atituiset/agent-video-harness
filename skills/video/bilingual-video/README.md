# bilingual-video

The **general layer for bilingual (zh+en) video production** with HyperFrames — independent of video type. Dual independent projects, edge-tts (Chinese) / Kokoro (English) narration with native word-boundary captions, the single-line iteration loop, publishing conventions, and 26 universal pitfalls. Route to a concrete workflow via `/hyperframes` first; this layer applies to all of them.

任何 HyperFrames 视频的中英双语生产通用层——与视频类型无关：双语独立工程、edge-tts（中文）/Kokoro（英文）配音与原生词边界字幕、单行重录迭代闭环、发布物料惯例、26 条通用踩坑清单。

## Install / 安装

```bash
npx skills add Atituiset/skills --skill bilingual-video
```

## Contents / 内容

| Path | What / 用途 |
|---|---|
| `SKILL.md` | The skill itself / 技能本体 |
| `scripts/gen-voice.py` | edge-tts narration with native word boundaries / edge-tts 原生词边界配音 |
| `references/pitfalls.md` | 26 universal pitfalls / 26 条通用踩坑清单 |

## Related / 相关

- `bilingual-tech-explainer`（同仓库）：技术科普视频特化层，依赖本技能。
