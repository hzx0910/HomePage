## ADDED Requirements

### Requirement: 主题色与待办开关配置存储
系统 SHALL 在 `homepage_config.settings` 中存储 `accentColor`（十六进制色值字符串）和 `showTodos`（boolean）字段。页面初始化时若字段不存在，SHALL 使用默认值（`accentColor: '#6366f1'`，`showTodos: true`）并向后兼容旧配置。

#### Scenario: 主题色写入配置
- **WHEN** 用户选择主题色
- **THEN** `homepage_config.settings.accentColor` 更新为对应色值并写入 localStorage

#### Scenario: 待办开关写入配置
- **WHEN** 用户切换待办显示开关
- **THEN** `homepage_config.settings.showTodos` 更新为对应 boolean 值并写入 localStorage

#### Scenario: 旧配置兼容补填
- **WHEN** 页面加载时 `settings` 缺少 `accentColor` 或 `showTodos` 字段
- **THEN** 系统用默认值补填缺失字段，不影响其他已存储数据
