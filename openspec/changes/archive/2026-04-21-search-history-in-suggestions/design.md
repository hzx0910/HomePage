## Context

`Suggestions.render(items)` 目前只渲染远程 JSONP 返回的联想词。`History.list()` 已提供完整历史数组。导出由 `Settings.export()` 直接序列化整个 `this.cfg`（即顶层 `config` 对象），其中包含 `searchHistory`。

## Goals / Non-Goals

**Goals:**
- 联想词列表顶部展示与输入词匹配的历史条目（包含输入词的子串匹配）
- 历史条目在联想词列表中可点击搜索、可删除（与历史视图一致）
- 导出 JSON 不含 `searchHistory`

**Non-Goals:**
- 历史条目参与键盘导航（保持简单，避免混合列表的导航复杂度）
- 历史与联想词之间的排序权重精调

## Decisions

### 决策 1：在 `Suggestions.render()` 内部注入历史

**采用**：`render(items)` 调用时，内部先查询 `History.list()`，过滤出包含当前查询词的条目（最多 3 条），在列表头部渲染为历史行（`.history-item` 样式），再渲染联想词行。  
**备选**：在 `fetch()` 回调处合并后传入 `render()`。  
**理由**：`render()` 已是唯一渲染入口，集中处理最省改动；同时 `fetch()` 不持有当前查询词的引用，在回调时需额外传参。

需要把当前查询词传给 `render()`，可通过新增参数 `render(items, query)` 实现，`query` 为空时不注入历史。

### 决策 2：历史条目上限 3 条

联想词最多 8 条，历史最多 3 条，总计不超过 11 条，视觉上不会过长。

### 决策 3：导出时用解构剔除 `searchHistory`

`export()` 中：`const { searchHistory, ...exportCfg } = this.cfg; JSON.stringify(exportCfg)`，零侵入，不影响内存中的 config 对象。

## Risks / Trade-offs

- [历史与联想词混排] 用户可能不清楚哪些是历史 → 历史条目复用 `.history-item` 样式（含删除按钮），视觉与联想词区分
- [render 签名变更] 现有所有 `render()` 调用需补传 `query` → 共 2 处（`fetch()` 回调、`focus` 恢复），改动极小
