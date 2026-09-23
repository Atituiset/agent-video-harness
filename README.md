# agent-video-harness

把技术文章做成**中英双语程序员科普视频**的开源工作流。基于 [HyperFrames](https://hyperframes.heygen.com)（HTML 即视频源）+ edge-tts/Kokoro 配音 + Whisper 级字幕对齐，全部流程可被任何 coding agent（Kimi Code / Claude Code / OpenCode / Codex 等）驱动。

实战产出（本仓库方法的完整案例）：《从一次 LLM 调用到完整 Harness，Agent 到底经历了什么？》双语科普视频（17 帧 / zh 3m33s / en 3m10s，覆盖 LLM→上下文→ReAct→工具调用→记忆→Harness 演化主线 + Pi/OpenCode/Codex/Hermes/Claude Code/DeepSeek Harness/Grok Build/Kimi Code 八家对比 + 九家定位总览图）。

## 特性

- **双语独立工程**：zh / en 各自独立时间轴，中文 edge-tts（晓晓）+ 英文 Kokoro（af_sky），字幕用 TTS 原生词边界对齐，不走 Whisper
- **连贯性三件套**：全片演化进度 rail、每帧 0.45s 开场舞台骨架、边界卡片母题——专治"赶场/幻灯片感"
- **叙事骨架**：撞墙 → 补墙（每一层工程复杂性的出现都有原因）
- **全套踩坑清单**：箭头三律、CJK 字体子集化、WCAG ghost text、seek 安全等 20+ 条实战规则
- **跨 agent 可复用**：技能是纯 Markdown + CLI 脚本，任何会跑 shell 的 agent 都能驱动（已实测 Kimi Code 与 OpenCode 互操作）

## 安装

前提：`npx hyperframes` CLI 可用（见 HyperFrames 文档）。

把技能装进你的 agent（任选其一）：

```bash
# Kimi Code / 通用 agents 目录
cp -r skills/bilingual-tech-explainer ~/.agents/skills/

# Claude Code
cp -r skills/bilingual-tech-explainer ~/.claude/skills/

# OpenCode
cp -r skills/bilingual-tech-explainer ~/.config/opencode/skills/
```

同时确保官方工作流在位：`npx skills add heygen-com/hyperframes --skill faceless-explainer`。

## 使用

对你的 agent 说：

> 读 bilingual-tech-explainer 技能，把这篇文章（附路径/链接）做成中英双语科普视频，
> 发布到 B站和 YouTube。工作目录 videos/<工程名>。

agent 会走官方 faceless-explainer 流水线（脚手架 → 设计预设 → 分镜脚本 → 配音 → 子代理建帧 → 装配 → 校验 → 渲染），差异层由技能接管。

配套资产：

| 路径 | 用途 |
|---|---|
| `skills/bilingual-tech-explainer/` | 技能本体（含 `scripts/gen-voice.py`，edge-tts 词边界配音） |
| `recipes/agent-harness-explainer/` | 冻结配方：code-editorial 设计预设 + 分镜骨架，新项目可直接采纳 |
| `examples/reference-case-frame.html` | 案例帧参考实现（见 `examples/README.md`） |
| `docs/pitfalls.md` | 完整踩坑清单（派任务前让 agent 先读） |

## 目录约定

```
videos/<name>-zh/   # 中文工程（先做，全流程）
videos/<name>-en/   # 英文工程（复制 zh 帧 → 翻译 → 按词边界重定时）
```

## License

MIT（见 LICENSE）。第三方字体文件（examples/assets/fonts/）保留各自原始许可证（EB Garamond / Inter / JetBrains Mono / Noto Sans SC 均为 OFL）。
