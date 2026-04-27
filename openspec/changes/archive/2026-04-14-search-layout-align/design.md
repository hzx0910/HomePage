## Context

当前 `#search-form` 使用 `display: flex; gap: 8px`，其中 `.search-input-wrap` 设置 `flex: 1`（占满剩余宽度），三个 `.engine-btn` 各自 `padding: 12px 16px`（宽度由内容决定）。整体 `#search-section` 与 `#main-grid` 同为 `max-width: 960px`，但内部比例与 grid 的 `3fr 1fr` 无关。

## Goals / Non-Goals

**Goals:**
- 搜索输入框区域宽度与 `#main-grid` 书签列（3fr）对齐
- 引擎按钮组宽度与 `#main-grid` 待办列（1fr）对齐
- 三个引擎按钮在按钮组内等宽、等距

**Non-Goals:**
- 不修改搜索功能逻辑
- 不修改引擎按钮的视觉样式（颜色、字体等）
- 不改变响应式断点行为

## Decisions

### 用 CSS grid 替代 flex 实现比例对齐

**决定**：将 `#search-form` 改为 `display: grid; grid-template-columns: 3fr 1fr; gap: 20px`，与 `#main-grid` 完全一致（同样的列比和间距），确保垂直对齐。

**理由**：直接复用与下方网格相同的 grid 定义，无需计算或 calc()，列宽天然对齐。

**备选方案**：用 `flex` + `calc(75% - 10px)` 等方式手动算宽度，但维护成本高，且 gap 不同时会有偏差。

### 引擎按钮组内部用 flex 等宽

**决定**：引擎按钮的父容器（即 grid 的第二列）内部使用 `display: flex; gap: 8px`，每个 `.engine-btn` 设置 `flex: 1` 实现等宽分布。

**理由**：flex + `flex: 1` 是实现等宽按钮最简洁的方式，无需指定具体宽度。

**实现方式**：在 HTML 中将三个 `.engine-btn` 包裹在一个 `<div id="search-engines">` 容器中，CSS 对该容器设置 flex。

## Risks / Trade-offs

- [低] grid gap 与原来 flex gap 从 8px 改为 20px（与主网格一致）会略微增大输入框与按钮组之间的间距 → 符合对齐意图，可接受
