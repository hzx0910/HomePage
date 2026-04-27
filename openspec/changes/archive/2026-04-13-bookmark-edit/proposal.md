## Why

书签添加后无法修改，用户若输错名称、URL 或分组，只能删除后重新添加，操作繁琐。新增编辑功能，让用户可以就地修改书签的分组、名称和链接。

## What Changes

- 书签悬浮/长按时，在左上角新增「编辑」按钮（原右上角已有删除叉号）
- 点击编辑按钮弹出编辑表单，支持修改分组、名称、链接
- 确认后更新书签数据并保存到 localStorage

## Capabilities

### New Capabilities

（无）

### Modified Capabilities

- `bookmarks`：书签新增编辑操作，可修改分组、名称、链接

## Impact

- 修改 `index.html` 书签渲染逻辑（书签 item HTML 加编辑按钮）
- 新增编辑弹窗/内联表单 HTML 结构
- 新增 CSS（编辑按钮定位样式）
- 新增 JS（编辑按钮事件、表单预填、保存逻辑）
