## Why

搜索联想词在用户点击其他区域（触发 blur）后被隐藏，同时 `_items` 缓存也被清空。用户再次点击输入框时，没有触发新的 `input` 事件，联想词无法重新显示，需要重新输入才能看到联想词，体验不连贯。

## What Changes

- `Suggestions.hide()` 拆分为「视觉隐藏」和「完全清空」两个行为：blur 时只隐藏不清空缓存，搜索完成/清空输入时才完全清空
- 输入框获得 focus 时，若缓存中有联想词，自动重新渲染显示

## Capabilities

### New Capabilities

（无新能力，为现有搜索联想词功能的行为修复）

### Modified Capabilities

- `search-suggestions`: 联想词隐藏/恢复行为变更——blur 时保留缓存，focus 时恢复显示

## Impact

- `index.html`：修改 `Suggestions.hide()` 逻辑；新增 `Suggestions.hideOnly()`（仅视觉隐藏）；在 `blur` 事件中改用 `hideOnly()`；新增 `focus` 事件监听器
