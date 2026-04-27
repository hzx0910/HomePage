## 1. HTML 结构

- [x] 1.1 将待办区域的输入框行（`#todo-input-row`）替换为「＋ 添加待办」按钮（`#todo-add-btn`）
- [x] 1.2 新增待办 modal HTML（`#todo-modal`），包含标题输入框（`#todo-title`）、链接输入框（`#todo-url`）、确认和取消按钮

## 2. CSS 样式

- [x] 2.1 为待办 item 添加悬浮显示编辑按钮的样式（复用 `.bm-edit` 定位规则）
- [x] 2.2 为有链接的待办标题添加链接样式（`.todo-link`：颜色继承，下划线）
- [x] 2.3 添加待办拖拽中和悬停的视觉样式（`.dragging` opacity，可复用已有规则）

## 3. JS — modal 与编辑

- [x] 3.1 在 Todos 模块中新增 `editingId` 状态变量
- [x] 3.2 新增 `openModal()` 方法：清空表单，设置确认按钮文字为"添加"，显示 modal
- [x] 3.3 新增 `openEditModal(t)` 方法：预填标题和链接，设置 `editingId`，确认按钮文字改为"保存"
- [x] 3.4 新增 `closeModal()` 方法：隐藏 modal，清空 `editingId`
- [x] 3.5 修改 `add()` → 重命名为 `save()`：区分新增和编辑模式，链接字段写入 `url`（可空），标题必填校验
- [x] 3.6 在 `init()` 中绑定添加按钮、modal 确认/取消/背景点击事件

## 4. JS — 渲染与链接

- [x] 4.1 修改 `makeItem(t)`：标题有 `t.url` 则渲染 `<a>` 链接，无则渲染 `<span>`
- [x] 4.2 在 `makeItem(t)` 中为未完成待办添加编辑按钮（悬浮显示，调用 `openEditModal`）
- [x] 4.3 移除旧的单行输入框相关事件绑定（`#todo-input` keydown、旧 `#todo-add-btn` click）

## 5. JS — 拖拽排序

- [x] 5.1 在 Todos 模块中新增 `dragState` 变量
- [x] 5.2 在 `makeItem(t)` 中为未完成待办添加 `draggable="true"` 和 `data-id` 属性
- [x] 5.3 为未完成待办绑定 `dragstart`、`dragend`、`dragover`、`drop` 事件（逻辑与书签拖拽一致）
- [x] 5.4 实现 `rebuildPendingFromDOM()`：从 `#todos-pending` DOM 顺序重建未完成待办数组顺序，保存到 localStorage
