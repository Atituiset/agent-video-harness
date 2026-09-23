# examples/

## reference-case-frame.html

一个案例帧的参考实现（来自实战项目的"Pi · 极简"帧），是新建案例帧时的抄写对象，覆盖：

- `<template>` 片段结构 + `data-composition-id` + 暂停的根 timeline 注册
- 案例舞台惯例：`✱ 案例 0N` kicker、顶部演化 rail（旅程点 + 案例点，当前 coral 高亮）
- 开场 0.45s 内立起舞台骨架（空槽位 + 空仪表盘），细节随配音词边界揭示
- 计数上升 + 环形扫描（count-up 签名动作）的 seek 安全写法
- 证据卡（真实测评截图）的进入时机与摆放

**注意**：这是结构/动效参考，不是可直接渲染的合成。它引用的 `assets/figures/*.png`
（真实文章测评截图）未包含在本仓库——请替换成你自己文章的证据图。
`assets/fonts/` 下的字体已包含（OFL 许可），子集化方法见 `docs/pitfalls.md` 第 19 条。
