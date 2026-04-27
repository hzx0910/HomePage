## ADDED Requirements

### Requirement: 编辑书签
用户 SHALL 能够编辑已有书签的分组、名称和链接。

#### Scenario: 触发编辑按钮
- **WHEN** 用户悬浮或长按某个书签
- **THEN** 书签左上角显示编辑按钮，右上角显示删除按钮

#### Scenario: 打开编辑表单
- **WHEN** 用户点击书签的编辑按钮
- **THEN** 弹出编辑表单，分组、名称、链接字段预填当前书签数据

#### Scenario: 保存编辑
- **WHEN** 用户修改字段后点击确认
- **THEN** 书签数据更新，列表重新渲染，变更保存到 localStorage

#### Scenario: 取消编辑
- **WHEN** 用户关闭编辑表单而不保存
- **THEN** 书签数据不变
