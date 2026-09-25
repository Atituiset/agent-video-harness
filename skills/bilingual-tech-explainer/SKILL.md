---
name: bilingual-tech-explainer
description: 把技术文章/调研文档做成中英双语程序员科普视频。叙事骨架（撞墙→补墙）+ 连贯性三件套（演化 rail / 开场舞台骨架 / 边界卡片）+ 科普专用的蓝图与证据卡模式。依赖同仓库的 bilingual-video 技能（配音/字幕/发布通用层）和官方 faceless-explainer 工作流。Use when turning a technical article, research notes, or docs into a bilingual (zh+en) explainer video for programmers.
---

# 双语技术科普视频（技术文章 → 中英科普片）

**依赖**：同仓库的 `bilingual-video` 技能（双语生产通用层：双工程、配音字幕、迭代闭环、发布惯例、26 条踩坑清单——先读它的 `references/pitfalls.md`）+ 官方 `/faceless-explainer` 工作流（`npx skills add heygen-com/hyperframes --skill faceless-explainer`）。本技能只定义科普片特有的叙事与视觉层。

自带资产（`<SKILL_DIR>` 为本技能目录）：
- `recipes/agent-harness-explainer/` — 冻结配方（code-editorial 设计预设 + BRIEF 骨架 + 分镜骨架），可被官方 `recipe.mjs use` 采纳或手动拷贝 `frame.md`
- `examples/reference-case-frame.html` — 案例帧参考实现（结构/计时/rail/字幕避让的抄写对象，见 `examples/README.md`）

## 叙事骨架：撞墙 → 补墙

技术演化/原理解构类内容，每一层必须"先撞墙再补墙"：上一层的能力边界先被点名（"模型不记得上一轮——这是第一条边界"），再引出本层机制。写 SCRIPT.md 时逐帧自查：本帧开场是否回答了"为什么现在讲这个"。案例之间要有转向句（"另一条路是…""X 关心的是另一件事：…"），否则就是赶场视频。

## 连贯性三件套（多帧科普的默认件）

1. **演化 rail**：顶部进度 rail（y≈48），全片每帧 t=0 就位、全程静止。层级段显示层级节点（过去=实心、当前=accent 大点+标签、未来=空心）；案例段切换为旅程点+案例点。它是全片共享的视觉锚点——幻灯片感的主要解药。
2. **开场舞台骨架**：每帧 t≤0.45s 必须已显示 kicker+完整标题+图解骨架（空槽位/底图）。官方注入的 0.5s 转场落在下一帧开头——没有骨架，观众反复看到空白画布。VO-paced reveal 只留给细节层。
3. **边界卡片**：每层开场亮 `✗ 边界 N · …`，机制落地时翻 accent ✓+删除线。把叙事铺垫可视化，不听配音也能看懂因果链。

## 科普片的内容模式

- **蓝图选择**：概念命名 → `kinetic-type-beats`/`typewriter-reveal`；机制层 → `grid-card-assemble`/`comparison-split`/`agent-progress-theater`；环形流程 → 自绘环 + 巡游点；案例/数据 → `dataviz-countup`；收尾论断 → `kinetic-type-beats` 接力 + 长驻。
- **证据卡**：源文章的测评截图/数据图是案例帧最好的可信素材（存 `_files/` 目录时先扫图片，别只提文字）。以带框卡片 + mono 图注（来源 · 日期）在数字落地后进入。
- **系列案例 + 总览**：多个平行案例用同一舞台（kicker 编号 + rail 进度），只换图解内容；收尾用一张定位图/对照表总览全部对象（"同一道题，只有取舍"），再落论断。
- **程序员审美**：终端/代码面可用深色面板 + mono 字体；克制 accent 色（每帧至多一处）；无背景音乐时可以完全静音标记（`music: none`）。
