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

### Requirement: 待办链接跳转
有链接的待办 SHALL 在新标签页打开对应 URL。

#### Scenario: 点击有链接的待办
- **WHEN** 用户点击有链接待办的标题
- **THEN** 系统在新标签页打开该链接

#### Scenario: 无链接待办不可点击
- **WHEN** 待办没有链接
- **THEN** 标题显示为普通文字，不可点击跳转

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

### Requirement: 待办区域宽度
待办区域 SHALL 占用约原来一半的宽度，在页面下方布局中与书签区并排时显示为较窄的列。

#### Scenario: 待办区域较书签区更窄
- **WHEN** 页面正常加载
- **THEN** 待办区域宽度约为原来的一半，书签区占用剩余主要空间

### Requirement: 待办复选框样式
待办复选框 SHALL 使用与页面主题一致的自定义样式，未选中和选中态均融入深色主题，不使用浏览器默认白色背景。

#### Scenario: 未选中态外观
- **WHEN** 待办事项未完成（未勾选）
- **THEN** 复选框显示为方形圆角，透明背景，`--text-muted` 边框，无白色填充

#### Scenario: 选中态外观
- **WHEN** 待办事项已完成（已勾选）
- **THEN** 复选框显示为方形圆角，主题色填充背景，白色勾号图标
