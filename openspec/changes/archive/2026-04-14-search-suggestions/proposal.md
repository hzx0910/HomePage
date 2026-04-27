## Why

用户在搜索框输入关键词时，缺乏即时的搜索联想词提示，导致搜索效率低下。通过接入搜索引擎免费 API 提供实时联想词，可显著提升搜索体验。

## What Changes

- 搜索框输入时，在其下方动态展示搜索联想词列表
- 联想词通过当前默认搜索引擎的免费 Suggestions API 获取
- 点击联想词直接触发搜索，跳转至对应搜索引擎结果页
- 支持键盘导航（上下方向键选择，Enter 确认，Escape 关闭）
- 失去焦点或搜索完成后自动收起联想词列表

## Capabilities

### New Capabilities

- `search-suggestions`: 搜索联想词下拉列表，包括数据获取、展示、交互及键盘导航

### Modified Capabilities

- `search-box`: 搜索框需监听输入事件并与联想词列表联动（触发请求、管理焦点状态）

## Impact

- `index.html`：新增联想词列表 DOM 元素、样式及交互逻辑
- 外部依赖：各搜索引擎的 JSONP/公开 Suggestions API（如 Google、百度、Bing）
- 无需修改 localStorage 数据结构
