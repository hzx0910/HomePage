## Why

输入关键词时，联想词列表只来自远程 JSONP API，用户自己搜索过的相关词被完全忽略；同时搜索历史作为个人数据不应随配置一起导出，以免隐私泄露或导入到其他环境时污染历史。

## What Changes

- 联想词列表渲染前，先从搜索历史中筛选出**包含当前输入词**的条目，将其插入列表最前面（历史条目与联想词视觉上区分）
- 历史条目在联想词列表中同样支持点击搜索，并显示删除按钮
- 导出配置时从导出对象中剔除 `searchHistory` 字段，使其不出现在 JSON 文件里

## Capabilities

### New Capabilities

（无新能力，均为对现有能力的行为修改）

### Modified Capabilities

- `search-suggestions`: 渲染联想词时，将匹配的历史条目前置合并展示
- `search-history`: 导出配置不包含 `searchHistory`

## Impact

- `index.html`：`Suggestions.render()` 增加历史前置逻辑；`Settings.export()` 导出时剔除 `searchHistory` 字段
