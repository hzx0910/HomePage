## Requirements

### Requirement: 基本搜索
搜索框 SHALL 接受用户输入，通过三个引擎按钮（百度、Bing、Google）或按 Enter 键触发搜索，结果在新标签页打开。点击任意引擎按钮执行该引擎的搜索，同时将其设为新的默认引擎。搜索框 SHALL 监听 `input` 事件以驱动联想词列表的显示与隐藏。搜索执行后，搜索框内容 SHALL 保留（不清空）。

#### Scenario: 点击引擎按钮搜索
- **WHEN** 用户在搜索框输入关键词后点击某个引擎按钮
- **THEN** 系统在新标签页打开该引擎的搜索结果页，并将该引擎设为默认，联想词列表关闭，搜索框内容保留

#### Scenario: Enter 键使用默认引擎
- **WHEN** 用户在搜索框输入关键词并按 Enter，且联想词列表无键盘高亮项
- **THEN** 系统在新标签页打开当前默认引擎的搜索结果页，联想词列表关闭，搜索框内容保留

#### Scenario: 空输入不触发
- **WHEN** 用户在空搜索框按 Enter 或点击任意引擎按钮
- **THEN** 系统不跳转，不做任何操作

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

### Requirement: 搜索引擎可配置
系统 SHALL 支持通过配置定义搜索引擎列表（百度、Bing、Google），每个引擎包含名称和 URL 模板（`{q}` 为查询占位符）。

#### Scenario: 读取配置中的搜索引擎
- **WHEN** 页面加载
- **THEN** 搜索框使用配置中 `search.defaultEngine` 指定的引擎作为默认高亮按钮

### Requirement: 搜索框清空按钮
搜索输入框内右侧 SHALL 显示一个圆形叉号清空按钮。该按钮仅在输入框有内容时可见，无内容时隐藏。点击后清空输入框并将焦点保留在输入框。

#### Scenario: 有内容时显示清空按钮
- **WHEN** 用户在搜索框中输入任意字符
- **THEN** 清空按钮出现在输入框内右侧

#### Scenario: 无内容时隐藏清空按钮
- **WHEN** 搜索框为空（包括初始状态和清空后）
- **THEN** 清空按钮不可见

#### Scenario: 点击清空按钮
- **WHEN** 用户点击清空按钮
- **THEN** 搜索框内容被清空，焦点回到搜索框，清空按钮随即隐藏
