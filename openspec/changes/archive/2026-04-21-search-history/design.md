## Context

当前 `Search.doSearchWithQueryAndEngine` 执行搜索后会主动清空输入框并移除 `has-value` class。`Suggestions` 模块负责联想词的获取和渲染，当输入为空时隐藏下拉列表。

本次变更需要在不引入新依赖、不改变整体架构的前提下，在单文件纯静态应用中增加搜索历史功能。

## Goals / Non-Goals

**Goals:**
- 搜索后保留输入框中的查询词
- 将每次搜索的关键词写入 localStorage，最多 10 条，去重并最新置顶
- 空输入框聚焦时在联想词下拉区域展示搜索历史
- 支持单条历史删除

**Non-Goals:**
- 历史记录的云同步
- 历史记录的搜索/过滤
- 跨浏览器标签共享历史

## Decisions

### 决策 1：复用 Suggestions 下拉框渲染历史

**选项 A（采用）**：在 `Suggestions` 模块内增加 `renderHistory(items)` 路径，历史条目与联想词共享同一个 `#search-dropdown` DOM 元素，通过 CSS class 区分样式。  
**选项 B**：新建独立的历史下拉 DOM 元素，完全分离。  
**理由**：选项 A 代码量少，位置对齐逻辑复用，且下拉只有一个不会互相遮挡；选项 B 需要重复大量定位和键盘导航逻辑。

### 决策 2：搜索历史存储在顶层 config 对象

将 `searchHistory: []` 加入 `DEFAULT_CONFIG`，统一通过 `Storage.save(config)` 持久化，与现有 `bookmarks`、`todos` 保持一致，支持整体导出/导入。

### 决策 3：空输入聚焦时触发历史展示

在 `input` 的 `focus` 事件处理中：若输入框为空且历史非空，调用 `Suggestions.renderHistory()`；若输入框非空，走原有缓存恢复逻辑。  
`input` 事件处理中：若输入框变为空（用户全部删除），隐藏联想词并改为展示历史。

### 决策 4：搜索后不清空输入框

去掉 `doSearchWithQueryAndEngine` 末尾的 `inp.value = ''` 和 `classList.remove('has-value')` 两行，保留内容。  
清空按钮行为不变——用户仍可手动点击 × 清空，此时恢复历史展示逻辑。

## Risks / Trade-offs

- [历史与联想词同框] 用户可能混淆历史和联想词 → 历史条目加"历史"图标或不同背景色区分，右侧加删除 × 按钮
- [搜索后不清空] 用户执行多次连续搜索时体验变化 → 输入框仍保留上次词，用户可快速修改，符合浏览器地址栏惯例
- [localStorage 空间] 10 条历史极小，不存在容量问题
