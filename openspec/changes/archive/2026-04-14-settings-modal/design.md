## Context

当前「设置」按钮展开一个内联 `#bg-panel`，只有两个操作按钮。需要容纳三项配置（背景图、主题色、待办开关），内联面板空间不足且视觉凌乱。项目是纯静态单文件 HTML，已有 modal 组件模式（书签/待办弹窗），复用即可。

## Goals / Non-Goals

**Goals:**
- 设置弹窗复用现有 modal 样式体系
- 主题色以 CSS 变量 `--accent` / `--accent-hover` 驱动，覆盖范围与现有半透明方案保持一致
- 待办开关即时生效，书签区动态占满全宽

**Non-Goals:**
- 不支持自定义输入任意色值（仅预设色板）
- 不做响应式适配（项目本身无移动端需求）

## Decisions

### 决策 1：弹窗复用现有 `.modal-backdrop` / `.modal` 结构

**理由**：已有样式和交互模式，直接复用保持一致性，无需引入新组件。

### 决策 2：主题色用 CSS 变量实时切换

**选择**：点选色板后，通过 `document.documentElement.style.setProperty('--accent', value)` 同时设置 `--accent` 和 `--accent-hover`（亮色版），`body.has-bg` 下的半透明覆盖规则保持不变（`--accent` 被覆盖为 rgba 版），无需额外处理。

**预设色板（6 色）**：
- 靛蓝 `#6366f1`（默认，当前 accent）
- 紫罗兰 `#8b5cf6`
- 玫瑰 `#f43f5e`
- 橙 `#f97316`
- 青绿 `#14b8a6`
- 天蓝 `#3b82f6`

每个颜色同时定义对应的 hover 亮色（lightness +10%）。

### 决策 3：待办开关用 CSS class 切换布局

**选择**：`body` 加/去 `hide-todos` class，CSS 中针对此 class 将 `#main-grid` 的 `grid-template-columns` 改为 `1fr`，`#todos-card`（待办卡片）`display: none`。

**理由**：纯 CSS 驱动，无需操作 DOM 结构，JS 只需切换 class 并存储状态。

### 决策 4：settings 存储结构扩展

```json
{
  "settings": {
    "backgroundImage": null,
    "accentColor": "#6366f1",
    "showTodos": true
  }
}
```

旧配置缺失字段时使用默认值，向后兼容。

## Risks / Trade-offs

- **`body.has-bg` 与主题色半透明的叠加**：`body.has-bg` 中覆盖的 `--accent` 为 rgba，而 `documentElement` 上设置的是 hex。由于 `body.has-bg` 的规则优先级更高（选择器更具体），有背景图时自动应用 rgba 版本，无背景图时使用 hex 版本，行为符合预期。需要在切换主题色时同时更新 `body.has-bg` 规则对应的 rgba 值——通过动态更新 CSS 变量解决：设置 `--accent-rgb`（r,g,b 三分量），`body.has-bg` 用 `rgba(var(--accent-rgb), 0.75)` 引用。

## Migration Plan

旧配置 `settings` 缺少 `accentColor` / `showTodos` 时，`Storage.init()` 补填默认值：`accentColor: '#6366f1'`，`showTodos: true`。
