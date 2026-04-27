## 1. 联想词列表注入历史条目

- [x] 1.1 修改 `Suggestions.render(items)` 签名为 `render(items, query)`，`query` 默认为空字符串
- [x] 1.2 在 `render()` 内，当 `query` 非空时，从 `History.list()` 筛选包含 `query` 的条目（最多 3 条），在列表头部以 `.history-item` 样式渲染（含删除按钮），再渲染远程联想词
- [x] 1.3 更新 `fetch()` 回调中的 `this.render(items)` 调用，改为 `this.render(items, query)`（`query` 即当前输入词）
- [x] 1.4 更新 `focus` 恢复逻辑中的 `Suggestions.render(Suggestions._items)` 调用，保持传空 `query`（不注入历史，避免历史重复显示）

## 2. 导出配置剔除 searchHistory

- [x] 2.1 修改 `Settings.export()`：导出前用解构 `const { searchHistory, ...exportCfg } = this.cfg` 剔除 `searchHistory`，序列化 `exportCfg` 而非 `this.cfg`
