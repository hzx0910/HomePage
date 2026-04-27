## Requirements

### Requirement: 搜索区域与主内容区等宽
搜索区域 SHALL 与主内容区（书签+待办）宽度一致，最大宽度均为 1024px，视觉上左右对齐。搜索栏内部列宽比例 SHALL 与主内容网格（3fr 书签列 + 1fr 待办列）一致，使搜索输入框与书签区垂直对齐，引擎按钮组与待办区垂直对齐。

#### Scenario: 搜索区宽度对齐
- **WHEN** 页面正常加载
- **THEN** 搜索框区域与下方书签/待办区域左右边界对齐

#### Scenario: 搜索输入框与书签列对齐
- **WHEN** 页面正常加载
- **THEN** 搜索输入框（含清空按钮）的右边界与书签区的右边界垂直对齐

#### Scenario: 引擎按钮组与待办列对齐
- **WHEN** 页面正常加载
- **THEN** 引擎按钮组的左右边界与待办区的左右边界垂直对齐

#### Scenario: 引擎按钮等宽等距
- **WHEN** 页面正常加载
- **THEN** 三个引擎按钮宽度相同，间距相同，充满按钮组区域

### Requirement: 待办区域宽度比例
待办区域 SHALL 占主内容区约 25%（grid 比例 3:1），书签区占约 75%。

#### Scenario: 待办列较书签列更窄
- **WHEN** 页面正常加载
- **THEN** 书签区宽度约为待办区的三倍

### Requirement: 待办隐藏时书签全宽布局
当 `settings.showTodos` 为 false 时，主内容区 `#main-grid` SHALL 切换为单列布局，书签卡片占满全宽；待办卡片 SHALL 隐藏不占位。

#### Scenario: 隐藏待办时书签全宽
- **WHEN** `settings.showTodos` 为 false
- **THEN** `#main-grid` 变为单列（`grid-template-columns: 1fr`），书签卡片宽度占满整个内容区

#### Scenario: 显示待办时恢复双列
- **WHEN** `settings.showTodos` 为 true
- **THEN** `#main-grid` 恢复为 `3fr 1fr` 双列布局，书签和待办卡片并排显示

### Requirement: 窄屏断点下布局行为
在视口宽度 ≤ 600px 的断点下，页面布局 SHALL 自动切换为适合手机使用的单列堆叠结构，桌面双列布局要求仅在宽屏（> 600px）下生效。

#### Scenario: 桌面双列布局仅在宽屏生效
- **WHEN** 视口宽度 > 600px
- **THEN** 搜索区 `3fr 1fr` 双列、主内容区 `3fr 1fr` 双列均正常显示

#### Scenario: 窄屏覆盖双列规则
- **WHEN** 视口宽度 ≤ 600px
- **THEN** 所有双列 Grid 布局被单列覆盖，内容垂直堆叠
