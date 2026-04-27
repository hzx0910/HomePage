## 1. CSS 样式

- [x] 1.1 为书签 item 左上角编辑按钮添加绝对定位样式（与右上角删除按钮对称）

## 2. HTML 结构

- [x] 2.1 在书签 item 渲染逻辑中，于左上角插入编辑按钮（`.bm-edit`）

## 3. Modal 复用（编辑模式）

- [x] 3.1 在 Bookmarks JS 模块中新增 `editingId` 状态变量（null = 新增模式，有值 = 编辑模式）
- [x] 3.2 新增 `openEditModal(bm)` 方法：预填 modal 表单字段，设置 `editingId`，更新确认按钮文字为"保存"
- [x] 3.3 修改 modal 确认逻辑：若 `editingId` 有值则更新现有书签，否则执行原有新增逻辑；保存后清空 `editingId`

## 4. 事件绑定

- [x] 4.1 在书签 item 渲染时为编辑按钮绑定点击事件，调用 `openEditModal`
