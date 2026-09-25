---
name: bilingual-video
description: 任何 HyperFrames 视频的中英双语生产通用层——双语独立工程、edge-tts（中文）/Kokoro（英文）配音与原生词边界字幕、单行重录迭代闭环、发布物料惯例、26 条通用踩坑清单。与具体视频类型无关，任何路由（explainer/promo/recut/motion-graphics…）都先过这一层。Use when producing any bilingual (zh+en) video with HyperFrames, regardless of video type.
---

# 双语视频生产通用层（任何视频类型）

这是所有双语视频生产的**通用底座**，与视频类型无关。先按 `/hyperframes` 的 intent 层路由到具体工作流（faceless-explainer / product-launch-video / pr-to-video / talking-head-recut / embedded-captions / music-to-video / motion-graphics / general-video），本技能提供它们之上不变的五样东西。

技术科普视频请直接用同仓库的 `bilingual-tech-explainer`（它依赖本技能）。

## 1. 双工程，不参数化

中英建两个独立工程 `videos/<name>-zh` / `videos/<name>-en`。配音时长差可达 15%，时间轴各自独立才不拧巴。顺序：**先做 zh 全流程到 render；EN 工程复制 zh 的 `compositions/frames/` 后逐帧翻译 + 按英文词边界重定时**——reveal 必须 re-anchor 到被念到的词，禁止均匀缩放。镜像修改要做两遍、验两遍。

## 2. 配音与字幕（与视频类型无关）

- **中文**：edge-tts `zh-CN-XiaoxiaoNeural --rate=+3%`（Kokoro 中文音色有口音，英文却很好）。用 `scripts/gen-voice.py`——edge-tts 的 `boundary="WordBoundary"` 原生词边界直接产出官方管线兼容的 `audio_meta.json`，免 Whisper：
  ```bash
  python3 -m venv scripts/.venv && scripts/.venv/bin/pip install edge-tts fonttools brotli
  scripts/.venv/bin/python <SKILL_DIR>/scripts/gen-voice.py --project .          # 全部行
  scripts/.venv/bin/python <SKILL_DIR>/scripts/gen-voice.py --project . 3 4 5    # 只重录改动行（merge）
  ```
- **英文**：官方音频管线 + Kokoro `af_sky` `--speed 1.05`（需 `pip install kokoro-onnx soundfile`，`HYPERFRAMES_PYTHON` 指向 venv）。
- Kokoro/edge-tts 均确定性输出。两侧都用官方 `audio.mjs sync-durations` 回写分镜时长、`captions.mjs` 出字幕。

## 3. 迭代闭环（改稿的最小成本路径）

改一行文案 → 只重录该行（merge 模式）→ `sync-durations` → 只重定时该帧（reveal re-anchor 到新词边界）→ 重建该帧字幕 → `assemble-index` + `transitions inject` → `lint`/`check` → 重渲。单行修改总成本几分钟，不要整片重来。

## 4. 交付与发布惯例

- 终检：ffmpeg 抽每帧收尾时刻 + 若干转场接缝目检；文件体积是快速健康指标（几 MB 的全隐形残片 = 时间轴结构坏了）。
- 封面：抽高光帧，`crop=1920:890` + `pad` 回 1080 裁掉字幕带。
- B站：科技→计算机技术，简介带章节时间轴 + 素材署名，投自制。YouTube：Chapters 时间轴、Science & Technology、勾选 Altered content（合成配音披露）。
- **发布前必须人工试听配音**（尤其中英混读词），模型无法亲耳验证。

## 5. 踩坑清单（26 条，全部通用）

`<SKILL_DIR>/references/pitfalls.md`：配音/字幕、合成/时间轴、动效/seek 安全、文字/对比度、工作流/协作五类。派发任务给任何 agent（或自己动手）前先读。
