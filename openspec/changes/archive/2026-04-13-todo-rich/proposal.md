## Why

当前待办只支持纯文本，无法关联链接。用户有时需要在待办中记录一个网页链接（如需处理的文档、工单、参考资料），点击即可直接跳转。同时待办顺序固定，无法拖拽调整优先级，也无法修改已添加的内容。

## What Changes

- 待办添加方式改为 modal 弹窗，包含标题（必填）和链接（选填）两个字段
- 有链接的待办，标题以可点击链接形式展示，点击在新标签页打开
- 待办支持拖拽排序（仅未完成列表）
- 待办支持编辑（修改标题和链接）
- 待办数据结构新增 `url` 字段（可选）

## Capabilities

### New Capabilities

（无）

### Modified Capabilities

- `todos`：添加方式、数据结构、展示交互均发生变化

## Impact

- 修改 `index.html` 待办区域 HTML（输入框改为添加按钮 + modal）
- 新增待办 modal HTML（标题 + 链接字段）
- 修改 Todos JS 模块（add、makeItem、render 逻辑）
- 修改待办 CSS（有链接时标题样式、拖拽样式、编辑按钮）
- localStorage 中 todos 数组每项新增可选 `url` 字段（向后兼容）
