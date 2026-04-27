## MODIFIED Requirements

### Requirement: 添加待办
用户 SHALL 能够通过弹窗添加新的待办事项，填写标题（必填）和链接（选填）。

#### Scenario: 打开添加弹窗
- **WHEN** 用户点击添加待办按钮
- **THEN** 弹出包含标题和链接字段的 modal

#### Scenario: 成功添加（无链接）
- **WHEN** 用户填写标题后确认
- **THEN** 新待办出现在未完成列表顶部，仅显示标题文字，数据保存到 localStorage

#### Scenario: 成功添加（有链接）
- **WHEN** 用户填写标题和链接后确认
- **THEN** 新待办出现在未完成列表顶部，标题显示为可点击链接，数据保存到 localStorage

#### Scenario: 空标题不添加
- **WHEN** 用户提交空标题
- **THEN** 系统不添加新条目

## ADDED Requirements

### Requirement: 待办链接跳转
有链接的待办 SHALL 在新标签页打开对应 URL。

#### Scenario: 点击有链接的待办
- **WHEN** 用户点击有链接待办的标题
- **THEN** 系统在新标签页打开该链接

#### Scenario: 无链接待办不可点击
- **WHEN** 待办没有链接
- **THEN** 标题显示为普通文字，不可点击跳转

### Requirement: 编辑待办
用户 SHALL 能够编辑已有待办的标题和链接。

#### Scenario: 触发编辑
- **WHEN** 用户悬浮到某个待办
- **THEN** 显示编辑按钮

#### Scenario: 打开编辑表单
- **WHEN** 用户点击编辑按钮
- **THEN** 弹出编辑 modal，标题和链接字段预填当前数据

#### Scenario: 保存编辑
- **WHEN** 用户修改后确认
- **THEN** 待办数据更新，保存到 localStorage

### Requirement: 待办拖拽排序
未完成的待办 SHALL 支持拖拽排序，新顺序 SHALL 持久化到 localStorage。

#### Scenario: 拖拽调整顺序
- **WHEN** 用户拖拽某个未完成待办到另一位置
- **THEN** 待办顺序更新，数据保存到 localStorage
