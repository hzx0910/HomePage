## 1. HTML 结构

- [x] 1.1 将 `#search-form` 中的三个 `.engine-btn` 包裹到新容器 `<div id="search-engines">` 中

## 2. CSS 样式

- [x] 2.1 将 `#search-form` 改为 `display: grid; grid-template-columns: 3fr 1fr; gap: 20px`（移除原 flex 声明）
- [x] 2.2 移除 `.search-input-wrap` 的 `flex: 1`（grid 子元素自动填充列宽）
- [x] 2.3 为 `#search-engines` 添加 `display: flex; gap: 8px`，并将 `.engine-btn` 设置 `flex: 1`
