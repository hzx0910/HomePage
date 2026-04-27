## ADDED Requirements

### Requirement: 待办隐藏时书签全宽布局
当 `settings.showTodos` 为 false 时，主内容区 `#main-grid` SHALL 切换为单列布局，书签卡片占满全宽；待办卡片 SHALL 隐藏不占位。

#### Scenario: 隐藏待办时书签全宽
- **WHEN** `settings.showTodos` 为 false
- **THEN** `#main-grid` 变为单列（`grid-template-columns: 1fr`），书签卡片宽度占满整个内容区

#### Scenario: 显示待办时恢复双列
- **WHEN** `settings.showTodos` 为 true
- **THEN** `#main-grid` 恢复为 `3fr 1fr` 双列布局，书签和待办卡片并排显示
