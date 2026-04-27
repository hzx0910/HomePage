## Why

待办事项的复选框在未选中状态下显示浏览器默认的白色背景，与页面整体深色主题格格不入。`accent-color` 属性只能控制选中态颜色，无法统一未选中态外观。需要用自定义样式替换原生 checkbox，使选中和未选中态均融入主题风格。

## What Changes

- 隐藏原生 `input[type="checkbox"]`，用纯 CSS 自定义复选框组件替代
- 未选中：透明/深色背景 + 主题色边框，圆角圆形或方形
- 选中：主题色填充背景 + 白色勾号图标
- 两态均使用主题色（`--accent`），视觉风格统一

## Capabilities

### New Capabilities

（无新能力，仅视觉样式调整）

### Modified Capabilities

- `todos`: 复选框视觉样式变更——从原生 checkbox 改为自定义主题风格组件

## Impact

- `index.html`：修改 `.todo-item input[type="checkbox"]` 相关 CSS；需配合 HTML 结构调整（隐藏原生 input + 添加自定义指示器元素，或纯 CSS 方案）
- 不影响 checkbox 的 `checked` 状态逻辑和事件绑定
