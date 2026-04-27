## ADDED Requirements

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

#### Scenario: 导出包含背景图
- **WHEN** 用户点击导出配置且已设置背景图
- **THEN** 导出的 JSON 文件中包含 `settings.backgroundImage` Base64 字段
