---
format: 1920x1080
duration: 230s
arc: concept-explainer with process
music: none
---

## Video direction

**Palette system（roles → hues，全部取自 frame.md，禁止发明）**

- 地景：warm cream `#FAF9F5` 为默认地面；内容聚拢在 half-step 的 tile `#EFE9DE` / tile-strong 上——永不纯白、永不冷灰。
- 声音：ink `#141413` 承载全部标题与正文；navy 面上反转为 cream。
- 电压：coral `#CC785C` 每帧恰好一处（一次下划线描边 / 一个巡游亮点 / 一道信封边），✱ kicker 作为固定 chrome 不计入；coral 永不排标题或正文。
- 代码面：warm navy `#181715` / `navy-soft` / `navy-elev` 只用于终端与代码面板（cream@14% 发丝边）；语法 coral / teal `#5DB8A6` / amber `#E8A55A` 是固定装饰色，不进品牌三色。
- 字体按角色引用：display = EB Garamond 400 sentence-case，**中文 display 行走预设记录的 CJK fallback——Noto Serif SC**；body = Inter / Noto Sans SC；index · kicker · code = JetBrains Mono（Latin 标识符）/ Noto Sans Mono CJK。display 句脊负字距，kicker 全大写 0.16em 带 coral ✱。
- 海拔只靠 1px 发丝边 + 至多一团柔和暖影；无重投影、无辉光、无渐变、无倾斜。
- 字幕带：底部 ~17% 为字幕保留区，一切内容规划进上 83%；居中 hero 锚在 y≈0.42×H 而非画面正中；背景/氛围层可全幅。

**Motion grammar + reveal model**

- 长尾 `power3` 缓动为默认，smooth 胜于 bouncy；overshoot 不出场。
- VO-paced reveal：t=0 只出现 VO 此刻正在说的东西；每一条线、每一层、每张卡都在被念到的那一刻才揭示，reveals 铺满整段时长、尤其后 50%；任何帧不得前 25% 倾倒全部内容。
- hold 期间唯一合法的活性是 subtle jitter（低幅 `sine-wave-loop`）；禁止懒惰呼吸、禁止后半段缓慢 pan/push——宁可静止不要坏运动。
- 帧内接缝一律速度匹配（velocity-matched cut）；帧间转场由 story 的 `transition_in` 注入，本层不碰。
- 案例序列（Frame 08–11）统一舞台：左上 kicker "✱ 案例 0N" + 名称·主题行，帧间一律 push-slide LEFT 接缝，只有图解内容逐帧更换。

**Held / breather allocation（刻意的静帧节奏）**

- **Frame 7 后三分之一**（11.0–13.0s）：zoom-out 锁定后的 Harness 全景完全静读——题眼命名后的呼吸。
- **Frame 12 末拍**（11.5–13.0s）：结论行长驻收尾，全片最后一个 held read。
- 其余帧全部按 VO 逐拍揭示，每帧结尾都落在 held read 上。

**Negative list**

- 两种失败形态都禁止：slideshow（前 25% 倾倒后冻结）与 screensaver（多元素各自漂浮装"活"）。
- 禁止紫蓝"AI"渐变、漂浮 bokeh、通用装饰图形冒充设计过的隐喻。
- 禁止真实浏览器 chrome / 真实光标 UI；本片无界面截图，一切视觉为发明图形。
- 禁止 bounce/elastic 默认入场；禁止 coral 双电压；禁止纯白/冷灰/第四品牌色。

## Frame 1 — Hook：像操作系统的 Agent

- duration: 8.496s
- transition_in: cut
- status: outline
- src: compositions/frames/01-hook.html
- type: hook
- persuasion: Counterintuitive claim
- beat: intrigue
- blueprint: typewriter-reveal (Adapt)
- focal: 逐字敲出的 `answer = LLM(question)` 等宽代码行
- roles: 打字行 + 光标 = foreground subject（居中唯一亮部）· 四层系统外壳轮廓 = background（dim ~35%，环抱层）· navy 终端场域 = background 地景

<fill in: this video's content for the "Hook：像操作系统的 Agent" beat — keep the layout role, replace the words.>

## Frame 2 — LLM：一个纯函数

- duration: 11.064s
- transition_in: crossfade
- status: outline
- src: compositions/frames/02-llm.html
- type: product_intro
- persuasion: Concretization
- beat: clarity
- blueprint: prompt-type-submit-generate (Adapt)
- focal: 标着 LLM 的方块与穿过它的 token 芯片流
- roles: LLM 方块 + token 流 = foreground subject（约占画面 50%）· navy 代码面板 = supporting（提问/作答载体）· "无记忆 / 无世界" mono 标注 = supporting · cream 地 = background

<fill in: this video's content for the "LLM：一个纯函数" beat — keep the layout role, replace the words.>

## Frame 3 — Q&A Bot：上下文装配层

- duration: 16.392s
- transition_in: push-slide LEFT
- status: outline
- src: compositions/frames/03-context.html
- type: feature_showcase
- persuasion: Progressive disclosure
- beat: comprehension
- blueprint: grid-card-assemble (Adapt)
- focal: 三张上下文卡片收拢成请求信封并入块的装配动作
- roles: 三卡 + 信封 = foreground subject（triptych 约占 50%）· LLM 方块（延续 Frame 2）= supporting（右栏退暗）· kicker + display 短题 = supporting chrome · tile 地 = background

<fill in: this video's content for the "Q&A Bot：上下文装配层" beat — keep the layout role, replace the words.>

## Frame 4 — ReAct：行动闭环

- duration: 16.728s
- transition_in: push-slide LEFT
- status: outline
- src: compositions/frames/04-react.html
- type: feature_showcase
- persuasion: Demonstration
- beat: "aha"
- blueprint: agent-progress-theater (Adapt)
- focal: Thought→Action→Observation 三角环与环上巡游的 coral 亮点
- roles: 环形图解 = foreground subject（左区约占 50%）· navy while 伪代码面板 = supporting（右栏，行高亮与节点同步）· 节点 mono 标签 + "最早的 Agent 运行时" 标注 = supporting

<fill in: this video's content for the "ReAct：行动闭环" beat — keep the layout role, replace the words.>

## Frame 5 — Tool Calling：动作协议

- duration: 14.016s
- transition_in: push-slide LEFT
- status: outline
- src: compositions/frames/05-tools.html
- type: feature_showcase
- persuasion: Before/after
- beat: confidence
- blueprint: comparison-split (Adapt)
- focal: 右侧结构化三层流水线卡（Schema / Router / Result）
- roles: 左右双卡 = foreground subject（split-screen，右卡视觉权重略高）· 漂移解析文本 + 警告状态词 = supporting（左卡内）· 三层标签 + 对勾 + 连接发丝线 = supporting（右卡内）

<fill in: this video's content for the "Tool Calling：动作协议" beat — keep the layout role, replace the words.>

## Frame 6 — Memory：分层记忆

- duration: 11.472s
- transition_in: push-slide LEFT
- status: outline
- src: compositions/frames/06-memory.html
- type: feature_showcase
- persuasion: Analogy
- beat: comprehension
- blueprint: grid-card-assemble (Adapt)
- focal: 装满溢出的上下文窗口条与通往外部存储的分流路径
- roles: 上下文窗口条 + 溢出 token 块 = foreground subject（左区）· 长期记忆容器 = foreground 副角（右区）· 三张记忆类型卡 = supporting（容器内横排）· 双空间标注 = supporting

<fill in: this video's content for the "Memory：分层记忆" beat — keep the layout role, replace the words.>

## Frame 7 — Harness：外层运行时

- duration: 15.528s
- transition_in: zoom-through
- status: outline
- src: compositions/frames/07-harness.html
- type: benefit_highlight
- persuasion: Frame-then-fill
- beat: fascination
- blueprint: zoom-out-workspace-reveal (Adapt)
- focal: 拉远后显形的 Harness 六壳运行时全景（约占画面 55%）
- roles: 中心 Agent Loop（Frame 4 的环）= foreground 起点 · 六块外壳面板 = foreground subject · "Harness" display 命名 + coral 下划线 = foreground 落点 · 外壳间发丝连线 + mono 标签 = supporting

<fill in: this video's content for the "Harness：外层运行时" beat — keep the layout role, replace the words.>

## Frame 8 — 案例 Pi：极简

- duration: 10.296s
- transition_in: push-slide LEFT
- status: outline
- src: compositions/frames/08-pi.html
- type: social_proof
- persuasion: Statistical proof
- beat: surprise
- blueprint: dataviz-countup (Adapt)
- focal: 66.7% 主 number-lockup（计数升起 + 字形随值放大）
- roles: 两组 number-lockup = foreground subject（3:1 大小层级）· 四枚工具徽章 = foreground 副角（大面积留白即论点）· 案例 kicker + 名称行 = supporting chrome

<fill in: this video's content for the "案例 Pi：极简" beat — keep the layout role, replace the words.>

## Frame 9 — 案例 OpenCode：事件驱动

- duration: 12.48s
- transition_in: push-slide LEFT
- status: outline
- src: compositions/frames/09-opencode.html
- type: social_proof
- persuasion: Demonstration
- beat: comprehension
- blueprint: transcript-scroll-artifact-reveal (Adapt)
- focal: 事件流向下汇入 SQLite 投影卡的纵贯线
- roles: 事件行流 = foreground subject（居中偏右竖列）· SQLite 投影卡 = foreground 落点 · 原始回复气泡 = supporting 引子 · 生命周期刻度签 + Compaction 高亮 = supporting

<fill in: this video's content for the "案例 OpenCode：事件驱动" beat — keep the layout role, replace the words.>

## Frame 10 — 案例 Codex：安全边界

- duration: 14.52s
- transition_in: push-slide LEFT
- status: outline
- src: compositions/frames/10-codex.html
- type: social_proof
- persuasion: Causal chain
- beat: conviction
- blueprint: compose
- focal: 命令芯片穿越 Approval × Sandbox 双闸门的水平通道
- roles: 命令芯片 + 双闸门 + 范围环 = foreground subject（full-width strip 横贯中上部）· Thread/Turn/Item 生命周期树 = supporting（右下栏，明确不做成统计图）· 对勾 + mono 标签 = supporting

<fill in: this video's content for the "案例 Codex：安全边界" beat — keep the layout role, replace the words.>

## Frame 11 — 案例 Hermes：自进化

- duration: 8.544s
- transition_in: push-slide LEFT
- status: outline
- src: compositions/frames/11-hermes.html
- type: social_proof
- persuasion: Generalization
- beat: foresight
- blueprint: compose
- focal: 经验回流闭环（任务 → Archive → Review → Memory/Skills → 下一任务）
- roles: 环形回流图解 = foreground subject（centered，约占 50%）· 弯路/直路对比细线 = supporting（暗淡 vs 亮起）· 归档堆叠行 + 蒸馏中间态 = supporting

<fill in: this video's content for the "案例 Hermes：自进化" beat — keep the layout role, replace the words.>

## Frame 12 — 案例 Claude Code：完备度上限

- duration: 11.616s
- transition_in: push-slide LEFT
- status: outline
- src: compositions/frames/12-claude.html
- type: social_proof
- persuasion: Demonstration
- beat: mastery
- blueprint: compose

<fill in: this video's content for the "案例 Claude Code：完备度上限" beat — keep the layout role, replace the words.>

## Frame 13 — 案例 DeepSeek Harness：事件总线

- duration: 10.296s
- transition_in: push-slide LEFT
- status: outline
- src: compositions/frames/13-deepseek.html
- type: social_proof
- persuasion: Concretization
- beat: comprehension
- blueprint: grid-card-assemble

<fill in: this video's content for the "案例 DeepSeek Harness：事件总线" beat — keep the layout role, replace the words.>

## Frame 14 — 案例 Grok Build：自愈可靠性

- duration: 8.832s
- transition_in: push-slide LEFT
- status: outline
- src: compositions/frames/14-grok.html
- type: social_proof
- persuasion: Demonstration
- beat: confidence
- blueprint: compose

<fill in: this video's content for the "案例 Grok Build：自愈可靠性" beat — keep the layout role, replace the words.>

## Frame 15 — 案例 Kimi Code：调度自己

- duration: 9.624s
- transition_in: push-slide LEFT
- status: outline
- src: compositions/frames/15-kimi.html
- type: social_proof
- persuasion: Analogy
- beat: fascination
- blueprint: constellation-hub

<fill in: this video's content for the "案例 Kimi Code：调度自己" beat — keep the layout role, replace the words.>

## Frame 16 — 总览：九家一张图

- duration: 18.768s
- transition_in: crossfade
- status: outline
- src: compositions/frames/16-overview.html
- type: benefit_highlight
- persuasion: Frame-then-fill
- beat: foresight
- blueprint: dataviz-countup

<fill in: this video's content for the "总览：九家一张图" beat — keep the layout role, replace the words.>

## Frame 17 — 落点：被边界逼出来的系统

- duration: 14.688s
- transition_in: crossfade
- status: outline
- src: compositions/frames/12-landing.html
- type: branding
- persuasion: Callback + Distillation
- beat: "now I get it"
- blueprint: kinetic-type-beats (Adapt)
- focal: 收束结论长句（display 级中文衬线，近全幅）
- roles: 三拍接力短句 = foreground subject（逐拍独占画面）· 结论两行 = foreground 落点 · 顶部迷你索引栈（三句回放）= supporting

<fill in: this video's content for the "落点：被边界逼出来的系统" beat — keep the layout role, replace the words.>
