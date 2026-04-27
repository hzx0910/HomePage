## MODIFIED Requirements

### Requirement: 默认配置
系统 SHALL 内置一套默认配置，用于首次使用时初始化数据。`settings` 默认值 SHALL 包含 `fontSize: 3`。

#### Scenario: 首次使用初始化
- **WHEN** 用户首次打开页面且 localStorage 中无配置数据
- **THEN** 系统使用内置默认配置初始化（包含常用搜索引擎和示例书签），`settings.fontSize` 默认为 3

#### Scenario: 旧配置兼容补填 fontSize
- **WHEN** 页面加载时 `settings` 缺少 `fontSize` 字段
- **THEN** 系统用默认值 3 补填缺失字段，不影响其他已存储数据
