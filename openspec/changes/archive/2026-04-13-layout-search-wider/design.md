## Context

页面垂直布局：搜索区在上（居中，`max-width: 620px`），主内容区在下（`max-width: 960px`，grid 2fr/1fr）。两者均通过 `margin: 0 auto` 居中对齐。

## Goals / Non-Goals

**Goals:**
- 搜索区 `max-width` 与主内容区对齐（同为 960px）
- 待办列更窄（grid 比例 3fr:1fr）

**Non-Goals:**
- 不做响应式断点调整
- 不改变搜索框内部元素布局

## Decisions

### 搜索区宽度

**决定**：将 `#search-section` 的 `max-width: 620px` 改为 `max-width: 960px`，与 `#main-grid` 一致。

**理由**：两者使用相同 `max-width` 后，居中对齐时左右边界自然对齐，视觉整洁。搜索 form 内部已是 `flex`，输入框会自动拉伸填满。

### 待办区比例

**决定**：`grid-template-columns` 从 `2fr 1fr` 改为 `3fr 1fr`，待办列占整体约 25%。

**理由**：待办内容相对简单，不需要太宽；书签数量多，更宽的书签区能展示更多内容。

## Risks / Trade-offs

- [低] 待办列更窄后，输入框和待办文字可能在极端情况下截断 → 可接受，待办内容通常较短
