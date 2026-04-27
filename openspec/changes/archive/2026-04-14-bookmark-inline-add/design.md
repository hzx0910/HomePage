## Context

当前书签卡片和待办卡片各有一行 `.card-header`，分别包含标题文字和操作按钮。添加书签的 `#bm-add-btn` 位于书签卡片标题行右侧。书签通过 `Bookmarks.render()` 动态生成，末尾无内联添加入口。

## Goals / Non-Goals

**Goals:**
- 隐藏书签和待办的 `.card-header`，减少视觉噪音
- 在书签渲染时于最后一个分组的 `.bm-group-items` 末尾插入内联 ＋ 按钮
- 点击内联按钮触发现有添加弹窗逻辑（复用 `Bookmarks.openAddModal()`）

**Non-Goals:**
- 不移除 `#bm-add-btn` DOM（隐藏 `.card-header` 后随之不可见即可，无需改 HTML）
- 不改变添加书签弹窗的逻辑和字段
- 不处理书签为空时的空态（空态已有单独的 `.empty-hint` 提示）

## Decisions

### 隐藏 card-header：CSS `display:none`

直接对书签卡片和待办卡片的 `.card-header` 加 `display: none`。因为是通用 class，需用子选择器精确定位：`#bookmarks-list` 的父 `.card` 和 `#todos-card` 内的 `.card-header`。更直接的方式是给两个卡片各自加 id，或直接对 `.card .card-header` 整体隐藏——但当前只有这两处用到 `.card-header`，可以直接全隐藏。

### 内联添加按钮插入时机：render() 末尾

在 `Bookmarks.render()` 的 groups 循环结束后，取最后一个分组的 `.bm-group-items`，append 一个 `.bm-inline-add` 按钮。这样每次 render 都会重建，不需要额外维护状态。

### 样式：与 `.bm-item` 视觉一致但更轻量

`.bm-inline-add` 使用虚线边框、`--text-muted` 颜色，hover 时加深，尺寸与 `.bm-item` 相似，宽度固定（不拉伸），保持行内排列感。

## Risks / Trade-offs

- 书签为空时 `render()` 提前 return，不会插入内联按钮。空态 `.empty-hint` 文案当前提示「点击 ＋ 添加」，需同步修改为其他引导（或去掉该提示中对 ＋ 按钮的引用）。
- 隐藏 `.card-header` 后卡片顶部 padding 会略显空旷，可通过微调卡片 padding-top 来优化。
