## MODIFIED Requirements

### Requirement: 基本搜索
搜索框 SHALL 接受用户输入，通过三个引擎按钮（百度、Bing、Google）或按 Enter 键触发搜索，结果在新标签页打开。点击任意引擎按钮执行该引擎的搜索，同时将其设为新的默认引擎。

#### Scenario: 点击引擎按钮搜索
- **WHEN** 用户在搜索框输入关键词后点击某个引擎按钮
- **THEN** 系统在新标签页打开该引擎的搜索结果页，并将该引擎设为默认

#### Scenario: Enter 键使用默认引擎
- **WHEN** 用户在搜索框输入关键词并按 Enter
- **THEN** 系统在新标签页打开当前默认引擎的搜索结果页

#### Scenario: 空输入不触发
- **WHEN** 用户在空搜索框按 Enter 或点击任意引擎按钮
- **THEN** 系统不跳转，不做任何操作

## ADDED Requirements

### Requirement: 三引擎按钮 UI
搜索区域 SHALL 固定显示三个引擎按钮：百度、Bing、Google，排列在搜索输入框右侧。默认引擎按钮 SHALL 以高亮样式（accent 色）区别于其他按钮。

#### Scenario: 页面加载显示默认高亮
- **WHEN** 页面加载
- **THEN** 配置中 `search.defaultEngine` 对应的按钮以高亮样式显示，其余两个为普通样式

#### Scenario: 切换默认引擎后高亮更新
- **WHEN** 用户点击非默认引擎按钮（触发搜索）
- **THEN** 该按钮变为高亮，原默认按钮恢复普通样式

### Requirement: 默认引擎持久化
用户点击引擎按钮后，所选引擎 SHALL 立即持久化为新的默认引擎，写入 localStorage，页面刷新后保持。

#### Scenario: 持久化默认引擎
- **WHEN** 用户点击某引擎按钮执行搜索
- **THEN** `homepage_config.search.defaultEngine` 更新为该引擎名称并写入 localStorage

#### Scenario: 刷新后默认引擎保持
- **WHEN** 用户切换默认引擎后刷新页面
- **THEN** 上次选择的引擎按钮仍显示为高亮

## REMOVED Requirements

### Requirement: 快捷词切换搜索引擎
**Reason**: 三按钮 UI 已直接暴露所有支持的引擎，快捷词机制冗余且与新 UI 逻辑耦合复杂。
**Migration**: 直接点击对应引擎按钮即可，无需记忆快捷词。
