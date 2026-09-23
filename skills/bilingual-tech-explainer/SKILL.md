---
name: bilingual-tech-explainer
description: 把技术文章/调研文档做成中英双语程序员科普视频的封装工作流。基于 HyperFrames 官方 faceless-explainer，叠加中文 edge-tts 配音、双语独立工程、连贯性三件套（演化 rail / 开场舞台骨架 / 边界卡片）和全部踩坑清单。Use when turning a technical article, research notes, or docs into a bilingual (zh+en) explainer video for programmers.
---

# 双语技术科普视频工作流

把一篇技术文章做成中英两支 1920×1080 科普视频。**核心流水线走官方 `/faceless-explainer` 技能**（先加载它和 `/hyperframes`；没有则 `npx skills add heygen-com/hyperframes --skill faceless-explainer`）。本技能只定义差异层，全部规则来自一次完整实战的返工沉淀，自包含、不依赖任何外部工程。

仓库自带三样配套资产（以 `<REPO>` 指代本仓库根目录）：
- `<REPO>/recipes/agent-harness-explainer/` — 冻结配方（设计预设 + BRIEF 骨架 + 分镜骨架），可用 `node <media-use>/scripts/recipe.mjs use --hyperframes . --name agent-harness-explainer` 采纳，或手动把 `frame.md` 拷入新工程
- `<REPO>/examples/reference-case-frame.html` — 案例帧参考实现（结构/计时/rail/字幕避让的抄写对象；详见 `<REPO>/examples/README.md`）
- `<REPO>/docs/pitfalls.md` — 完整踩坑清单（派发任务给任何 agent 时让它先读）

## 与官方工作流的差异

### 1. 双工程，不参数化

建两个独立工程 `videos/<name>-zh` 和 `videos/<name>-en`。配音时长差可达 15%，时间轴各自独立。顺序：先做 zh 全流程到 render，EN 工程复制 zh 的 `compositions/frames/` 后逐帧翻译+按英文词边界重定时（reveal 必须 re-anchor 到词，禁止均匀缩放）。

### 2. 配音与字幕

- **中文**：edge-tts `zh-CN-XiaoxiaoNeural --rate=+3%`（中文不要用 Kokoro，口音重）。用本技能 `scripts/gen-voice.py`——edge-tts 的 `boundary="WordBoundary"` 原生词边界直接生成官方管线兼容的 `audio_meta.json`，比 Whisper 对齐更准更省：
  ```bash
  python3 -m venv scripts/.venv && scripts/.venv/bin/pip install edge-tts fonttools brotli
  scripts/.venv/bin/python <SKILL_DIR>/scripts/gen-voice.py --project .          # 全部行
  scripts/.venv/bin/python <SKILL_DIR>/scripts/gen-voice.py --project . 3 4 5    # 只重录改动的行（merge 模式）
  ```
- **英文**：官方音频管线，Kokoro `af_sky` `--speed 1.05`（需 `pip install kokoro-onnx soundfile` 并用 `HYPERFRAMES_PYTHON` 指向该 venv）。Kokoro/edge-tts 均确定性输出，改稿只重录改动行。
- 两侧都用 `audio.mjs sync-durations` 回写分镜时长，再用官方 `captions.mjs` 生成字幕。

### 3. 连贯性三件套（多帧科普视频默认件）

观众对"赶场/幻灯片感"的投诉都靠这三件解决：

1. **演化 rail**：顶部一条进度 rail（y≈48，x 860–1780），全片每帧 t=0 就位、全程静止。层级段显示 `LLM·上下文·循环·…` 节点（过去=实心、当前=coral r8+标签、未来=空心）；案例段切换为旅程点+案例点。它是全片共享的视觉锚点——幻灯片感的主要解药。
2. **开场舞台骨架**：每帧 t≤0.45s 必须已显示 kicker+完整标题+图解骨架（空槽位/底图）。否则注入的 0.5s 转场会落在空白画布上——这是"不连贯"观感的第一来源。VO-paced reveal 只留给细节层（卡内容、数字、被念到的标签）。
3. **边界卡片**（叙事型视频）：每层开场亮 `✗ 边界 N · …`，机制落地时翻 coral ✓+删除线。把"每个零件的出现都有原因"直接画出来。

### 4. 图解规则（箭头三律等）

- 箭头终点距目标 ≥14px；箭头用显式 polygon 且在 DOM/SVG 顺序中排在节点之后（后画者在上）；方向按路径切线计算核对。不要用 SVG `marker-end`，不要用 GSAP `attr: stroke-dashoffset`（会被 CSS 声明覆盖，只剩端点）。
- 巡游亮点（tour dot）的停泊位置避开所有箭头。
- "飞入容器"的元素停靠在容器边缘，别飞到中心再淡出（hold 帧会读成舞台空了）。
- 文字一律实心颜色 ≥4.5:1（check 会采样动画中间态）；`mask-image` 渐隐会制造 ghost text 必然炸对比度，滚出元素用 `tl.set(opacity: 0)` 硬切，保留的行用实心降深色。
- `tl.set(el, {innerText})` 不是 seek 安全——状态翻转用堆叠双元素 + autoAlpha 交叉淡入。

### 5. 环境与工程陷阱

- 系统 Python 受 PEP 668 保护 → 工程内建 venv（`scripts/.venv`）。
- SCRIPT.md 帧标题必须半角括号 `(Frame N)`，全角会静默生成 0 行配音。
- DOM id/class 必须字母开头（`01-hook-bg` 会让 querySelectorAll 直接 SyntaxError，整帧脚本全灭）。
- CJK 字体用 `pyftsubset --text-file=<工程用字> --flavor=woff2` 子集化（16MB→~112KB），引用 `assets/fonts/*.woff2`；别写机器上没有文件的字体名。
- 每个全长 clip 独占一条 `data-track-index` lane，否则装配器拒绝。
- 分镜帧号重排必须用完整标题精确匹配替换（部分正则会先匹配到新插入的同名前缀帧块，字幕整段错位）；改完对账 帧号×时长×src。
- 大并行子代理 swarm（>10）易撞用量上限；撞了用 harness 的 resume 机制恢复，工作不丢。子代理的临时验证文件用完即删，别留在工程根目录（触发 multiple_root_compositions）。
- 保存的网页只提文字会丢掉全部图片——先扫 `_files/` 目录，真实测评截图是案例帧最好的证据卡。
- 绝对定位的装饰元素挂到 `#root` 直下，别放进带 `position:absolute` 的子容器（top 会相对它计算而飞出画布）。

### 6. 交付与发布惯例

- 成片抽帧终检：ffmpeg 抽每帧收尾时刻 + 若干转场接缝目检。
- 封面：抽高光帧，`crop=1920:890 + pad 回 1080` 裁掉字幕带。
- 发布物料：B站（科技→计算机技术，简介带章节时间轴+原文署名，自制）；YouTube（Chapters、Science & Technology、勾选 Altered content 合成配音披露）。
- 发布前必须人工试听配音（尤其中英混读词）。
