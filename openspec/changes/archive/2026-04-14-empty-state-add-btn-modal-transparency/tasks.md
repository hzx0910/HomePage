## 1. 书签空态替换

- [x] 1.1 在 `Bookmarks.render()` 中，将空态 `<div class="empty-hint">暂无书签</div>` 替换为 `<button class="bm-empty-add">＋ 添加书签</button>`，并绑定 click 事件调用 `this.openModal()`
- [x] 1.2 新增 `.bm-empty-add` 样式：虚线边框、`--accent` 边框色、`--text-muted` 文字色、宽度撑满容器（`width: 100%`）、适当内边距，hover 时文字变为 `--text`、边框变为 `--accent-hover`

## 2. 弹窗透明度调整

- [x] 2.1 将 `--modal-bg` 中 base 颜色的 alpha 从 `0.95` 降至 `0.85`：`color-mix(in srgb, var(--accent) 14%, rgba(13,15,23,0.85))`
