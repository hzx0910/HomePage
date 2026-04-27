## ADDED Requirements

### Requirement: 展示搜索联想词列表
系统 SHALL 在搜索框下方展示一个悬浮联想词列表。用户在搜索框输入内容后（防抖 300ms），系统向当前默认搜索引擎的 Suggestions API（JSONP）发起请求，并将返回的联想词渲染为可点击列表项。输入框为空时列表 SHALL 隐藏。

#### Scenario: 输入触发联想词请求
- **WHEN** 用户在搜索框输入非空内容，且停止输入超过 300ms
- **THEN** 系统向当前默认搜索引擎的 JSONP Suggestions API 发送请求，请求参数为当前输入内容

#### Scenario: 展示联想词
- **WHEN** JSONP 请求成功返回联想词数组
- **THEN** 搜索框正下方出现联想词列表，每个联想词占一行，列表宽度与搜索框对齐，最多展示 8 条

#### Scenario: 清空输入时隐藏列表
- **WHEN** 用户清空搜索框内容
- **THEN** 联想词列表立即隐藏，任何 pending 请求的结果被丢弃

#### Scenario: API 请求失败时静默处理
- **WHEN** JSONP 请求失败（网络错误、超时、API 不可用）
- **THEN** 联想词列表不显示，搜索框正常可用，无错误提示

### Requirement: 点击联想词触发搜索
系统 SHALL 允许用户点击联想词列表中的任意项，触发使用当前默认搜索引擎对该联想词的搜索，在新标签页打开结果页，同时关闭联想词列表。

#### Scenario: 点击联想词跳转搜索
- **WHEN** 用户点击联想词列表中某一项
- **THEN** 系统在新标签页打开当前默认搜索引擎对该联想词的搜索结果页，联想词列表关闭

### Requirement: 键盘导航联想词列表
系统 SHALL 支持通过键盘在联想词列表中导航和选择，以提升无鼠标操作效率。

#### Scenario: 方向键向下导航
- **WHEN** 联想词列表可见时，用户按下 ↓ 键
- **THEN** 高亮选中下一条联想词（循环至列表末尾后回到第一项），搜索框内容更新为该联想词

#### Scenario: 方向键向上导航
- **WHEN** 联想词列表可见时，用户按下 ↑ 键
- **THEN** 高亮选中上一条联想词（到达第一项后循环至末尾），搜索框内容更新为该联想词

#### Scenario: Enter 键确认联想词
- **WHEN** 联想词列表可见且某项被键盘高亮时，用户按下 Enter
- **THEN** 系统在新标签页打开当前默认搜索引擎对高亮联想词的搜索结果页，联想词列表关闭

#### Scenario: Escape 键关闭列表
- **WHEN** 联想词列表可见时，用户按下 Esc
- **THEN** 联想词列表关闭，搜索框保留当前内容，焦点仍在搜索框

### Requirement: 失去焦点时关闭列表
系统 SHALL 在搜索框失去焦点时关闭联想词列表，以避免遮挡页面其他内容。

#### Scenario: 搜索框失焦关闭列表
- **WHEN** 用户点击页面其他区域，搜索框失去焦点
- **THEN** 联想词列表在短暂延迟（150ms）后关闭，以确保点击联想词的事件能正常触发

### Requirement: 适配多搜索引擎 JSONP API
系统 SHALL 根据当前默认搜索引擎，自动选择对应的 JSONP Suggestions API endpoint，保证联想词来源与用户选择的搜索引擎一致。

#### Scenario: 默认引擎为 Google 时使用 Google API
- **WHEN** 默认搜索引擎为 Google 且用户输入关键词
- **THEN** 系统向 `https://suggestqueries.google.com/complete/search?client=firefox&q=<keyword>&callback=<fn>` 发请求

#### Scenario: 默认引擎为百度时使用百度 API
- **WHEN** 默认搜索引擎为百度且用户输入关键词
- **THEN** 系统向 `https://suggestion.baidu.com/su?wd=<keyword>&cb=<fn>` 发请求

#### Scenario: 默认引擎为 Bing 时使用 Bing API
- **WHEN** 默认搜索引擎为 Bing 且用户输入关键词
- **THEN** 系统向 `https://api.bing.com/qsonhs.aspx?type=cb&q=<keyword>&cb=<fn>` 发请求
