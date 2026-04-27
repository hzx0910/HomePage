## Why

当前「设置」功能以内联面板展开，空间有限，且随着设置项增加难以扩展。将其改为弹窗形式，并补充主题色选择和待办区域显示开关两项配置，让用户对页面外观有更完整的掌控。

## What Changes

- 「设置」按钮点击后打开弹窗，替代原内联 `#bg-panel` 面板
- 弹窗内整合原有背景图功能，新增：
  - **主题色选择**：提供一组预设颜色，用户点选后更新内容区域 accent 色
  - **待办区域显示开关**：关闭后隐藏待办卡片，书签区域扩展到全宽

## Capabilities

### New Capabilities

- `settings-modal`: 设置弹窗，包括弹窗打开/关闭、三项配置（背景图、主题色、待办显示开关）的交互与持久化

### Modified Capabilities

- `custom-background`: 背景图配置从内联面板迁移到设置弹窗内（行为不变，入口改变）
- `config-storage`: `settings` 对象新增 `accentColor`（字符串，十六进制色值）和 `showTodos`（boolean）字段
- `layout`: 主内容区网格列比例根据 `showTodos` 动态切换（3fr 1fr ↔ 1fr）

## Impact

- `index.html`：移除 `#bg-panel`，新增设置弹窗 DOM；新增主题色、待办开关逻辑
- localStorage：`homepage_config.settings` 增加 `accentColor`、`showTodos` 字段
