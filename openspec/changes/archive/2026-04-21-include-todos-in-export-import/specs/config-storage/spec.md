## MODIFIED Requirements

### Requirement: 导出配置
用户 SHALL 能够将当前所有配置数据导出为 JSON 文件下载到本地。导出内容 SHALL 包含 `bookmarks`、`todos`、`settings`、`search` 等所有顶层字段。

#### Scenario: 导出配置
- **WHEN** 用户点击导出按钮
- **THEN** 系统触发浏览器下载，文件名为 `homepage-config.json`，内容为当前配置的完整 JSON

#### Scenario: 导出包含待办项
- **WHEN** 用户点击导出按钮且存在待办事项
- **THEN** 导出的 JSON 文件中 `todos` 字段为包含所有待办项（含已完成）的数组

#### Scenario: 导出包含背景图
- **WHEN** 用户点击导出配置且已设置背景图
- **THEN** 导出的 JSON 文件中包含 `settings.backgroundImage` Base64 字段

### Requirement: 导入配置
用户 SHALL 能够从本地 JSON 文件导入配置，覆盖当前所有数据，包括待办项。

#### Scenario: 成功导入
- **WHEN** 用户选择合法的配置 JSON 文件并确认导入
- **THEN** 系统解析文件内容，写入 localStorage，并重新渲染页面（包含已恢复的待办列表）

#### Scenario: 导入恢复待办项
- **WHEN** 用户导入包含 `todos` 数组的合法配置文件
- **THEN** 页面重新渲染后待办列表显示已导入的全部待办项（未完成与已完成）

#### Scenario: 非法文件拒绝导入——缺少 todos 字段
- **WHEN** 用户选择的 JSON 文件不含 `todos` 字段或其值不为数组
- **THEN** 系统显示错误提示，不修改现有数据

#### Scenario: 非法文件拒绝导入——格式错误
- **WHEN** 用户选择的文件不是合法的配置 JSON 格式
- **THEN** 系统显示错误提示，不修改现有数据
