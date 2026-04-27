## Why

页面目前使用固定深色背景，缺乏个性化空间。支持用户导入本地图片作为页面背景，可以让首页更具个人风格，提升使用体验。

## What Changes

- 在页脚工具栏「导入」按钮右侧新增「设置」按钮
- 点击「设置」打开配置面板，支持选择本地图片作为页面背景
- 图片以 Base64 形式存储在 `localStorage` 中，刷新后持久保留
- 支持移除背景图，恢复默认深色背景
- 背景图以 `cover` 模式覆盖整个页面，叠加半透明遮罩保证内容可读性

## Capabilities

### New Capabilities

- `custom-background`: 自定义背景图能力，包括图片选择、存储、渲染及移除

### Modified Capabilities

- `config-storage`: settings 对象新增 `backgroundImage`（Base64 字符串或 null）字段，导入/导出配置时一并处理

## Impact

- `index.html`：新增「设置」按钮、配置面板 DOM、背景渲染逻辑
- localStorage：`homepage_config.settings.backgroundImage` 字段（Base64，可能较大）
- 无外部依赖
