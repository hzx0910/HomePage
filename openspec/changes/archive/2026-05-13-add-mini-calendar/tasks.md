## 1. 布局调整

- [x] 1.1 在 `#main-grid` 中将待办卡片和新月历包裹在 `#right-column` 容器中，设置 `display: flex; flex-direction: column; gap: 20px`
- [x] 1.2 更新 `body.hide-todos` 规则，隐藏整个 `#right-column` 而非仅 `#todos-card`

## 2. 月历 HTML 结构

- [x] 2.1 在 `#right-column` 内、`#todos-card` 上方添加月历 `.card` 容器，包含顶部导航栏（左箭头、年月文本、右箭头）和 7 列日历网格区域

## 3. 月历 CSS 样式

- [x] 3.1 添加月历顶部导航栏样式：年月居中显示，左右箭头按钮使用现有 `.btn-icon` 风格
- [x] 3.2 添加日历网格样式：`grid-template-columns: repeat(7, 1fr)`，周一~周日列头使用 `--text-muted` 色
- [x] 3.3 添加日期单元格样式：紧凑行高，今天高亮使用 `--accent` 背景 + 白色文字 + 圆形

## 4. 月历 JS 模块

- [x] 4.1 创建 `Calendar` 模块，包含 `init()`、`render()`、`prevMonth()`、`nextMonth()` 方法
- [x] 4.2 实现 `render()` 方法：计算当月天数、第一天星期几，生成日历网格，判断并高亮今天
- [x] 4.3 绑定左右箭头点击事件，调用 `prevMonth()` / `nextMonth()` 切换月份并重新渲染
- [x] 4.4 在 Boot 阶段调用 `Calendar.init()` 初始化月历
