## Context

当前首页由搜索、书签（3fr 列）和待办（1fr 列）组成，使用 `#main-grid` 的 `grid-template-columns: 3fr 1fr` 布局。待办区域为右侧单独的 `.card`。需要在待办卡片上方新增一个等宽的月历组件，两者垂直排列在右侧 1fr 列中。

## Goals / Non-Goals

**Goals:**
- 在待办卡片上方添加极简月历，与待办等宽
- 显示当月日历网格（周一~周日），高亮今天
- 支持点击左右箭头切换月份
- 风格与现有深色主题完全一致

**Non-Goals:**
- 不与待办系统集成（不在日历上标记有待办的日期）
- 不支持点击日期进行任何操作
- 不持久化用户当前浏览的月份（刷新回到当月）

## Decisions

### 布局方案：右侧列用嵌套容器包裹月历和待办

将月历和待办卡片包裹在一个 `#right-column` 容器中，使用 `display: flex; flex-direction: column; gap: 20px`。`#main-grid` 保持 `3fr 1fr` 不变。

**替代方案**：用 CSS Grid 的 subgrid 或多行布局 — 复杂度高，且 file:// 协议下浏览器兼容性不确定。

### JS 模块：独立的 Calendar 对象

创建一个 `Calendar` 模块（与 Search、Bookmarks、Todos 同级），负责渲染和月份切换。不需要持久化状态，刷新后始终显示当月。

### 日历网格：纯 CSS Grid 7 列布局

使用 `display: grid; grid-template-columns: repeat(7, 1fr)` 渲染日历。上月溢出日和下月溢出日不显示，留空格。

**替代方案**：显示上下月灰色日期 — 增加视觉噪音，与"极简"定位不符。

### 隐藏待办时月历也隐藏

当用户在设置中关闭待办区域时，整个右侧列（含月历）一并隐藏，保持行为一致。

## Risks / Trade-offs

- **空间占用**：月历占据右侧列额外高度，待办区域可视空间减少 → 月历设计尽量紧凑，行高最小化
- **移动端适配**：600px 以下已有 `grid-template-columns: 1fr` 的响应式规则，月历自然排列在待办上方，无需额外处理
