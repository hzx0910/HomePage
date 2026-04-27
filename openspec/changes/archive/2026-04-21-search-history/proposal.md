## Why

搜索后搜索框被清空，用户无法看到刚才搜索的内容，也无法快速重复或修改查询；同时缺少搜索历史记录功能，用户无法找回之前的搜索关键词。

## What Changes

- 执行搜索后不再清空搜索框，保留搜索词
- 每次搜索时将关键词追加到搜索历史（localStorage），最多保留 10 条，重复词去重并置顶
- 搜索框为空时获得焦点，在联想词下拉区域展示搜索历史列表（复用联想词展示框）
- 搜索历史列表每条右侧提供删除按钮，可单独删除某条历史

## Capabilities

### New Capabilities
- `search-history`: 搜索历史的存储、读取、去重、展示与删除

### Modified Capabilities
- `search`: 搜索执行后保留搜索框内容（不清空）
- `search-suggestions`: 输入框为空且获得焦点时展示搜索历史而非联想词；输入非空时仍走联想词流程

## Impact

- `index.html`：`Search.doSearchWithQueryAndEngine` 去掉清空输入框逻辑；`Suggestions` 模块扩展以支持历史列表的渲染与交互；`Storage` / `config` 增加 `searchHistory` 数组字段
- localStorage 结构新增 `searchHistory` 字段
