## Why

搜索栏与下方书签/待办区域宽度一致，但内部比例不对齐：搜索输入框未与书签区对齐，引擎按钮组也未与待办区对齐，视觉上缺乏整体感。用户希望搜索栏各部分在垂直方向上与下方的两列完全对齐。

## What Changes

- 搜索输入框（含清空按钮）宽度对齐书签区（占搜索行约 3/4）
- 右侧引擎按钮组宽度对齐待办区（占搜索行约 1/4）
- 三个引擎按钮在按钮组内等宽、等距分布

## Capabilities

### New Capabilities

（无）

### Modified Capabilities

- `layout`: 搜索栏内部列宽比例与主内容网格对齐的要求发生变化

## Impact

- 修改 `index.html` 中 `#search-form` 的 CSS：`search-input-wrap` flex 比例改为与书签列对齐，引擎按钮容器宽度固定与待办列对齐，按钮 `flex: 1` 实现等宽
