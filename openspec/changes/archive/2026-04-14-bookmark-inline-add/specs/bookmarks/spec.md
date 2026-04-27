## MODIFIED Requirements

### Requirement: 书签卡片布局
书签卡片 SHALL 隐藏标题行（`.card-header`），直接展示书签分组列表，无标题文字和独立添加按钮。待办卡片 SHALL 同样隐藏标题行。

#### Scenario: 书签卡片无标题行
- **WHEN** 页面正常加载
- **THEN** 书签卡片不显示「书签」标题和右侧 ＋ 按钮，内容区直接从书签分组开始

#### Scenario: 待办卡片无标题行
- **WHEN** 页面正常加载
- **THEN** 待办卡片不显示「待办」标题，内容区直接从添加待办按钮开始
