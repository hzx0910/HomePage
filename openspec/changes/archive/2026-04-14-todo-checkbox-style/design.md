## Context

当前待办复选框：`<input type="checkbox">` 配合 `accent-color: var(--accent)`。`accent-color` 在 Chromium 中只着色选中填充，未选中态仍是浏览器默认白色背景，深色页面下视觉突兀。

## Goals / Non-Goals

**Goals:**
- 未选中态：深色/透明背景 + `--accent` 色圆形边框
- 选中态：`--accent` 填充 + 白色 SVG 勾号
- 过渡动画自然，与页面其他交互一致

**Non-Goals:**
- 不改变 checkbox 的 JS 事件绑定和 `checked` 属性逻辑
- 不修改设置面板中的 `toggle-switch` 组件（不是本次范围）

## Decisions

### 方案：纯 CSS，隐藏原生 input + label::before 自定义指示器

**做法：**
1. 在 JS 的 `Todos.render()` 中，给每个 `<input type="checkbox">` 紧跟后添加一个 `<label class="todo-cb-label">` 元素，`for` 属性指向 checkbox 的动态 id（或直接用 `<label>` 包裹 input）
2. CSS 隐藏原生 input（`appearance: none; opacity: 0; position: absolute`），用 `label::before` 渲染自定义圆圈，`input:checked + label::before` 切换为填充+勾号

**备选（更简单）：** 直接对 `input[type="checkbox"]` 使用 `appearance: none` 并用 `::before` / background-image 实现，无需修改 JS HTML 结构。

**选择备选方案** — 纯 CSS，零 JS 改动：
- `appearance: none` 移除浏览器默认样式
- 未选中：`border: 1.5px solid var(--accent); border-radius: var(--radius-sm); background: transparent`
- 选中：`background: var(--accent); border-color: var(--accent)` + `background-image` 内联 SVG 勾号（白色）
- 尺寸 16×16px，与文字行高对齐

### 勾号 SVG

使用内联 `background-image: url("data:image/svg+xml,...")` 白色 checkmark，避免引入外部资源：

```css
background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 10 8' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M1 4l3 3 5-6' stroke='white' stroke-width='1.5' fill='none' stroke-linecap='round' stroke-linejoin='round'/%3E%3C/svg%3E");
```

## Risks / Trade-offs

- `appearance: none` 在所有现代浏览器（Chrome/Firefox/Safari）均支持，无兼容风险
- 纯 CSS 方案无需改动 JS，改动范围最小
