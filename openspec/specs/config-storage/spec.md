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

### Requirement: 默认配置
系统 SHALL 内置一套默认配置，用于首次使用时初始化数据。`settings` 默认值 SHALL 包含 `fontSize: 3`。

#### Scenario: 首次使用初始化
- **WHEN** 用户首次打开页面且 localStorage 中无配置数据
- **THEN** 系统使用内置默认配置初始化（包含常用搜索引擎和示例书签），`settings.fontSize` 默认为 3

#### Scenario: 旧配置兼容补填 fontSize
- **WHEN** 页面加载时 `settings` 缺少 `fontSize` 字段
- **THEN** 系统用默认值 3 补填缺失字段，不影响其他已存储数据

### Requirement: 背景图配置存储
系统 SHALL 在 `homepage_config.settings.backgroundImage` 中存储用户设置的背景图 Base64 字符串，无背景时值为 `null`。页面初始化时若该字段不存在，SHALL 视为 `null`（向后兼容）。

#### Scenario: 背景图写入配置
- **WHEN** 用户选择背景图
- **THEN** `homepage_config.settings.backgroundImage` 更新为图片的 Base64 Data URL 字符串并写入 localStorage

#### Scenario: 移除背景图写入配置
- **WHEN** 用户移除背景图
- **THEN** `homepage_config.settings.backgroundImage` 更新为 `null` 并写入 localStorage

#### Scenario: 旧配置兼容
- **WHEN** 页面加载时 `homepage_config` 中不含 `settings` 字段
- **THEN** 系统将 `settings` 初始化为 `{ backgroundImage: null }`，不影响其他数据

### Requirement: 主题色与待办开关配置存储
系统 SHALL 在 `homepage_config.settings` 中存储 `accentColor`（十六进制色值字符串）和 `showTodos`（boolean）字段。页面初始化时若字段不存在，SHALL 使用默认值（`accentColor: '#1e3a6e'`，`showTodos: true`）并向后兼容旧配置。

#### Scenario: 主题色写入配置
- **WHEN** 用户选择主题色
- **THEN** `homepage_config.settings.accentColor` 更新为对应色值并写入 localStorage

#### Scenario: 待办开关写入配置
- **WHEN** 用户切换待办显示开关
- **THEN** `homepage_config.settings.showTodos` 更新为对应 boolean 值并写入 localStorage

#### Scenario: 旧配置兼容补填
- **WHEN** 页面加载时 `settings` 缺少 `accentColor` 或 `showTodos` 字段
- **THEN** 系统用默认值补填缺失字段（`accentColor` 回退值为 `#8e8ea8`），不影响其他已存储数据
