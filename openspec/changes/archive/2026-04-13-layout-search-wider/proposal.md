## Why

搜索区域当前最大宽度为 620px，比下方书签+待办区域（960px）窄，视觉上不对齐，显得搜索框偏小。同时待办区域可以进一步缩窄，给书签留出更多空间。

## What Changes

- 搜索区域（`#search-section`）宽度与下方主内容区等宽（最大 960px）
- 待办区域比例进一步缩小（grid 从 `2fr 1fr` 调整为 `3fr 1fr`）

## Capabilities

### New Capabilities

（无）

### Modified Capabilities

（无，仅 CSS 数值调整，不涉及行为变更）

## Impact

- 修改 `index.html` 中 `#search-section` 的 `max-width`
- 修改 `#main-grid` 的 `grid-template-columns` 比例
