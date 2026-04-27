## Context

搜索区域当前结构：`<form>` 内有 `<input>` 和三个引擎按钮并排。清空按钮需叠加在输入框内部右侧，不占用外部布局空间。

## Goals / Non-Goals

**Goals:**
- 清空按钮绝对定位在输入框内右侧
- 有内容时显示，无内容时隐藏（`visibility` 或 `opacity` 控制，避免布局抖动）
- 点击清空输入框内容，焦点回到输入框

**Non-Goals:**
- 不做动画
- 不影响三个引擎按钮的布局

## Decisions

### 定位方式

**决定**：用一个 `<div class="search-input-wrap">` 包裹 `<input>`，清空按钮 `position: absolute` 定位在其右侧内部；输入框加足够的 `padding-right` 避免文字被按钮遮挡。

**理由**：不影响外层 flex 布局，按钮与输入框视觉对齐最自然。

### 显示/隐藏

**决定**：监听 `input` 事件，有内容时给 wrap 加 `.has-value` class，CSS 控制按钮 `opacity: 1`，无内容时 `opacity: 0; pointer-events: none`。

**理由**：用 opacity 不会引起布局重排，比 `display:none` 切换更平滑。

## Risks / Trade-offs

- [无] 改动极小，风险极低
