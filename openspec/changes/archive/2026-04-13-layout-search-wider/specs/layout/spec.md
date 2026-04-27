## MODIFIED Requirements

### Requirement: 搜索区域与主内容区等宽
搜索区域 SHALL 与主内容区（书签+待办）宽度一致，最大宽度均为 960px，视觉上左右对齐。

#### Scenario: 搜索区宽度对齐
- **WHEN** 页面正常加载
- **THEN** 搜索框区域与下方书签/待办区域左右边界对齐

### Requirement: 待办区域宽度比例
待办区域 SHALL 占主内容区约 25%（grid 比例 3:1），书签区占约 75%。

#### Scenario: 待办列较书签列更窄
- **WHEN** 页面正常加载
- **THEN** 书签区宽度约为待办区的三倍
