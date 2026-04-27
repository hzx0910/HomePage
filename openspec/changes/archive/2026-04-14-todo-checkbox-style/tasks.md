## 1. 自定义复选框样式

- [x] 1.1 将 `.todo-item input[type="checkbox"]` 的样式替换为自定义方案：`appearance: none`、`16×16px`、`border-radius: 50%`、`border: 1.5px solid var(--accent)`、`transparent` 背景、`cursor: pointer`、`flex-shrink: 0`、加 `transition` 过渡
- [x] 1.2 添加选中态样式 `.todo-item input[type="checkbox"]:checked`：`background: var(--accent)`、`border-color: var(--accent)`、内联 SVG 白色勾号作为 `background-image`、`background-size` 和 `background-repeat` 适当设置
