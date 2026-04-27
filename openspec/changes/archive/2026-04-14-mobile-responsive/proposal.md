## Why

页面当前为固定双列桌面布局，在手机等窄屏设备上搜索引擎按钮和双列内容区会严重溢出或挤压，无法正常使用。通过 CSS 媒体查询适配窄屏，让页面在手机上也能流畅操作。

## What Changes

- 窄屏（≤ 600px）时，搜索表单改为单列：搜索框占满全宽，引擎按钮组移到搜索框正下方
- 窄屏时，主内容区 `#main-grid` 改为单列，待办卡片堆叠到书签卡片下方
- 窄屏时，整体内边距和间距适当收窄，避免内容紧贴屏幕边缘

## Capabilities

### New Capabilities

- `responsive-layout`: 窄屏媒体查询响应式布局，覆盖搜索区和主内容区的断点行为

### Modified Capabilities

- `layout`: 现有布局规格新增窄屏断点下的布局要求

## Impact

- `index.html`：CSS 新增 `@media` 断点规则，无需修改 JS 或 HTML 结构
