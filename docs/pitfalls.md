# 踩坑清单（自包含版）

一次完整实战（技术长文 → 双语 17 帧科普视频，五轮返工）沉淀的全部规则。派任务给任何 agent 前让它先读这份文件。

## 配音与字幕

1. 中文 TTS 用 edge-tts `zh-CN-XiaoxiaoNeural --rate=+3%`；Kokoro 中文音色有口音，但其英文音色（af_sky 1.05x）很好。
2. edge-tts 的 `Communicate(..., boundary="WordBoundary")` 有原生词边界（默认是 SentenceBoundary，必须显式传），可直接生成官方管线兼容的 `audio_meta.json`（shape：`{bgm, voices:[{frame, path, duration_s, words:[{id,text,start,end}]}], sfx}`），比 Whisper 对齐更准更省。
3. SCRIPT.md 帧标题必须半角 `(Frame N)`——全角 `（Frame N）` 解析器匹配不到，静默生成 0 行配音。
4. Kokoro/edge-tts 输出是确定性的：改稿只重录改动的行并 merge 进 audio_meta.json，未改帧完全不用动。
5. 时长估算：中文约 4.5 字/秒偏乐观，信息密度高的技术科普会超 10-16%，storyboard 的 duration 记得同步更新。

## 合成与时间轴

6. 数字开头的 DOM id/class（`01-hook-bg`）让 querySelectorAll 直接 SyntaxError，整帧脚本全灭——必须字母开头。lint 的 `id_requires_css_escape` 警告是预兆。
7. 每个全长 clip 独占一条 `data-track-index` lane；同 lane 重叠会被装配器拒绝。
8. 嵌套 GSAP timeline 不会被采集引擎 scrub——整体平移时间轴用脚本机械平移所有 tween，不用嵌套。
9. 改帧号/重排分镜时，替换标题必须用完整标题精确匹配（部分正则会先匹配到新插入的同名前缀帧块，字幕整段错位）；改完对账 帧号×时长×src。
10. 绝对定位的装饰元素挂到 `#root` 直下；放进带 `position:absolute` 的子容器会相对它计算而飞出画布。

## 动效与 seek 安全

11. SVG 弧线动画别用 GSAP `attr: stroke-dashoffset`——CSS 同名声明会覆盖它，只剩端点（"断开的箭头"）。用 CSS 属性补间 `strokeDashoffset`。
12. 箭头三律：终点距目标 ≥14px；显式 polygon 三角形且 DOM 顺序在节点之后（后画者在上）；方向按路径切线计算核对。不用 SVG `marker-end`（refX 语义坑多）。
13. 巡游亮点（tour dot）的停泊位置避开所有箭头。
14. "飞入容器"的元素停靠在容器边缘留缝可见；飞到中心再淡出会让 hold 帧读成"舞台空了"。
15. `tl.set(el, {innerText})` 不是 seek 安全——状态翻转用堆叠双元素 + autoAlpha 交叉淡入淡出。
16. GSAP 的 onUpdate 轨道计算在 `seek()` 下会被跳过（suppressEvents）——轨道类运动用可 seek 的 transform 补间（如旋转父级 `<g>`）。

## 文字与对比度

17. 文字一律实心颜色 ≥4.5:1——check 会采样动画中间态，低透明度装饰文字必然炸 WCAG 审计。
18. `mask-image` 渐隐让滚出文字变 ghost text，对比度数学上必然崩（1:1），改颜色救不回来——滚出元素在越界瞬间 `tl.set(opacity: 0)` 硬切，需要保留的行用实心降深色（如 rgb(129,128,126)）。
19. CJK 字体：机器上没有文件的字体名别写进 font stack；用 `pyftsubset --text-file=<工程用字> --flavor=woff2` 子集化（16MB→~112KB）放进 `assets/fonts/` 并用 `@font-face` 引用。

## 工作流与协作

20. 系统 Python 受 PEP 668 保护 → 工程内建 venv（`scripts/.venv`）。Kokoro 需 `kokoro-onnx + soundfile` + `HYPERFRAMES_PYTHON` 指向 venv。
21. 保存的网页只提取正文会丢掉全部图片——先扫 `_files/` 目录；真实测评截图/数据图是案例帧最好的"证据卡"。
22. 转场落在下一帧的前 0.5s——每帧 t≤0.45s 必须立起舞台骨架（kicker+标题+图解骨架），否则观众反复看到空白画布。
23. 跨帧连续性靠全片共享的持久元素（顶部演化 rail），不靠转场。
24. 大并行子代理（>10）易撞用量上限；撞了用 resume 恢复。子代理的临时验证文件用完即删（工程根目录的散装 html 会触发 multiple_root_compositions）。
25. 并行子代理会互相覆盖共享 `snapshots/` 目录——抽帧验证后立即拷贝到私有路径。
26. 模型无法亲耳验证配音——发布前必须人工试听（尤其中英混读词），不满意按行重录 + 单帧重定时，成本几分钟。
