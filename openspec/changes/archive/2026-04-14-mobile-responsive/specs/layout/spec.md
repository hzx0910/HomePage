## ADDED Requirements

### Requirement: 窄屏断点下布局行为
在视口宽度 ≤ 600px 的断点下，页面布局 SHALL 自动切换为适合手机使用的单列堆叠结构，桌面双列布局要求仅在宽屏（> 600px）下生效。

#### Scenario: 桌面双列布局仅在宽屏生效
- **WHEN** 视口宽度 > 600px
- **THEN** 搜索区 `3fr 1fr` 双列、主内容区 `3fr 1fr` 双列均正常显示

#### Scenario: 窄屏覆盖双列规则
- **WHEN** 视口宽度 ≤ 600px
- **THEN** 所有双列 Grid 布局被单列覆盖，内容垂直堆叠
