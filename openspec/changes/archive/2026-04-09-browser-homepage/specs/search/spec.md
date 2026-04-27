## ADDED Requirements

### Requirement: 基本搜索
搜索框 SHALL 接受用户输入并在新标签页打开搜索结果。按下 Enter 键或点击搜索按钮触发搜索。

#### Scenario: 普通搜索
- **WHEN** 用户在搜索框输入关键词并按 Enter
- **THEN** 系统在新标签页打开默认搜索引擎的搜索结果页

#### Scenario: 空输入不触发
- **WHEN** 用户在空搜索框按 Enter
- **THEN** 系统不跳转，不做任何操作

### Requirement: 快捷词切换搜索引擎
搜索框 SHALL 支持通过前缀快捷词切换搜索引擎，格式为 `<prefix> <query>`。

#### Scenario: 使用快捷词搜索
- **WHEN** 用户输入 `gh claude` 并按 Enter（`gh` 为 GitHub 的快捷词）
- **THEN** 系统在新标签页打开 GitHub 搜索 `claude` 的结果页

#### Scenario: 无效快捷词回退默认
- **WHEN** 用户输入 `xx something`（`xx` 不是已配置的快捷词）
- **THEN** 系统使用默认搜索引擎搜索完整输入 `xx something`

### Requirement: 搜索引擎可配置
系统 SHALL 支持通过配置文件定义多个搜索引擎，每个引擎包含名称、快捷词和 URL 模板（`{q}` 为查询占位符）。

#### Scenario: 读取配置中的搜索引擎
- **WHEN** 页面加载
- **THEN** 搜索框使用配置中 `search.defaultEngine` 指定的引擎作为默认
