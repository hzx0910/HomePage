## 1. CSS 修改

- [x] 1.1 隐藏书签卡片和待办卡片的 `.card-header`：新增 CSS 规则 `.card .card-header { display: none; }`
- [x] 1.2 新增 `.bm-inline-add` 样式：虚线边框、`--text-muted` 颜色、与 `.bm-item` 相近的尺寸，hover 时边框变为 `--accent`、文字变为 `--text`
- [x] 1.3 微调卡片 `padding-top`：card-header 隐藏后卡片顶部间距略显偏大，可将 `.card` 的 padding-top 从 `20px` 减小为 `16px`

## 2. Bookmarks.render() 修改

- [x] 2.1 在 groups 循环结束后，取最后一个分组对应的 `.bm-group-items` 元素，append 一个 `button.bm-inline-add`，文字为「＋」，title 为「添加书签」
- [x] 2.2 给内联按钮绑定 click 事件：调用 `this.openAddModal()`（与原 `#bm-add-btn` 逻辑一致）
- [x] 2.3 修改空态提示文案：将 `'暂无书签，点击 ＋ 添加'` 改为 `'暂无书签'`（内联按钮在空态下不显示，无需引导）
