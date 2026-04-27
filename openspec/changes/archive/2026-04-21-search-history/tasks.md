## 1. 数据层：搜索历史存储

- [x] 1.1 在 `DEFAULT_CONFIG` 中添加 `searchHistory: []` 字段
- [x] 1.2 编写 `History.add(query)` 函数：去重置顶、截断至 10 条、调用 `Storage.save(config)`
- [x] 1.3 编写 `History.remove(query)` 函数：从数组删除指定词、调用 `Storage.save(config)`
- [x] 1.4 编写 `History.list()` 函数：返回 `config.searchHistory` 数组副本

## 2. 搜索执行：保留输入框内容

- [x] 2.1 删除 `Search.doSearchWithQueryAndEngine` 末尾的 `inp.value = ''` 和 `classList.remove('has-value')` 两行
- [x] 2.2 在 `Search.doSearchWithQueryAndEngine` 中调用 `History.add(query)` 记录历史

## 3. 历史列表 UI：复用 Suggestions 下拉框

- [x] 3.1 在 `#search-dropdown`（联想词容器）的 CSS 中添加历史条目 `.history-item` 样式（含右侧删除按钮 `.history-delete`）及列表标题 `.history-header` 样式
- [x] 3.2 在 `Suggestions` 模块中添加 `renderHistory(items)` 方法：清空容器、渲染标题行 + 历史条目列表（含删除按钮），并显示下拉
- [x] 3.3 为历史条目绑定点击事件：调用 `Search.doSearchWithQuery(text)` 并更新输入框内容
- [x] 3.4 为删除按钮绑定点击事件（阻止冒泡）：调用 `History.remove(text)`，刷新历史列表（空则隐藏下拉）

## 4. 触发逻辑：空输入时展示历史

- [x] 4.1 修改 `input` 的 `focus` 事件处理：若输入框为空且 `History.list().length > 0`，调用 `Suggestions.renderHistory()`；否则走原有联想词缓存恢复逻辑
- [x] 4.2 修改 `input` 的 `input` 事件处理：当 `input.value` 变为空时，隐藏联想词并展示历史（若有）；非空时走原有联想词 fetch 流程
- [x] 4.3 修改清空按钮（`search-clear`）的点击处理：清空后若历史非空，调用 `Suggestions.renderHistory()`

## 5. 初始化与数据迁移

- [x] 5.1 在 `Storage.load` 的 config 合并逻辑中确保旧数据（无 `searchHistory` 字段）能正确补全默认值 `[]`
