## ADDED Requirements

### Requirement: 配置持久化
系统 SHALL 将所有用户数据（搜索引擎配置、书签、待办）以 JSON 格式存储在 localStorage 的单一 key `homepage_config` 下。

#### Scenario: 数据自动保存
- **WHEN** 用户进行任何数据变更（增删书签、增删改待办、修改设置）
- **THEN** 系统立即将最新数据序列化并写入 localStorage

#### Scenario: 页面加载恢复数据
- **WHEN** 用户打开首页
- **THEN** 系统从 localStorage 读取配置并渲染页面，若无数据则使用内置默认配置

### Requirement: 导出配置
用户 SHALL 能够将当前所有配置数据导出为 JSON 文件下载到本地。

#### Scenario: 导出配置
- **WHEN** 用户点击导出按钮
- **THEN** 系统触发浏览器下载，文件名为 `homepage-config.json`，内容为当前配置的完整 JSON

### Requirement: 导入配置
用户 SHALL 能够从本地 JSON 文件导入配置，覆盖当前所有数据。

#### Scenario: 成功导入
- **WHEN** 用户选择合法的配置 JSON 文件并确认导入
- **THEN** 系统解析文件内容，写入 localStorage，并重新渲染页面

#### Scenario: 非法文件拒绝导入
- **WHEN** 用户选择的文件不是合法的配置 JSON 格式
- **THEN** 系统显示错误提示，不修改现有数据

### Requirement: 默认配置
系统 SHALL 内置一套默认配置，用于首次使用时初始化数据。

#### Scenario: 首次使用初始化
- **WHEN** 用户首次打开页面且 localStorage 中无配置数据
- **THEN** 系统使用内置默认配置初始化（包含常用搜索引擎和示例书签）
