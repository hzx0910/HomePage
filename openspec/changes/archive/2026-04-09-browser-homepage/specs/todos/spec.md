## ADDED Requirements

### Requirement: 展示待办列表
系统 SHALL 展示所有待办事项，区分未完成和已完成状态。

#### Scenario: 展示未完成待办
- **WHEN** 页面加载且存在未完成待办
- **THEN** 系统展示未完成待办列表，每项显示文字内容和勾选框

#### Scenario: 展示已完成待办
- **WHEN** 存在已完成的待办事项
- **THEN** 系统在已完成区域展示这些条目，带有删除线样式

### Requirement: 添加待办
用户 SHALL 能够快速添加新的待办事项。

#### Scenario: 添加待办
- **WHEN** 用户输入待办内容并按 Enter 或点击添加按钮
- **THEN** 新待办出现在未完成列表顶部，数据保存到 localStorage

#### Scenario: 空内容不添加
- **WHEN** 用户提交空内容
- **THEN** 系统不添加新条目

### Requirement: 完成待办
用户 SHALL 能够将待办事项标记为已完成，已完成记录保留在历史中。

#### Scenario: 勾选完成
- **WHEN** 用户勾选某待办的复选框
- **THEN** 该待办移至已完成区域，记录完成时间，数据更新到 localStorage

#### Scenario: 取消完成
- **WHEN** 用户取消勾选已完成的待办
- **THEN** 该待办恢复至未完成列表，清除完成时间

### Requirement: 删除待办
用户 SHALL 能够删除单个待办事项（包括已完成的）。

#### Scenario: 删除待办
- **WHEN** 用户点击某待办的删除按钮
- **THEN** 该待办从列表中永久移除，数据从 localStorage 更新
