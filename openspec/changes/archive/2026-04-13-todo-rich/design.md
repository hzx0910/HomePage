## Context

待办模块当前：单行输入框 + Enter/按钮快速添加，数据结构 `{ id, text, done, createdAt, doneAt }`。书签模块已有完整的 modal（`#bm-modal`）+ 编辑模式（`editingId`）+ HTML5 DnD 拖拽排序模式，可作为参考直接复用。

## Goals / Non-Goals

**Goals:**
- 添加待办改为 modal（标题必填，链接选填）
- 有链接的待办标题渲染为 `<a>` 可点击，无链接渲染为 `<span>`
- 未完成待办支持 HTML5 DnD 拖拽排序（已完成区不支持）
- 待办支持编辑（修改标题/链接）
- 数据结构向后兼容（旧数据无 `url` 字段正常展示）

**Non-Goals:**
- 已完成待办不支持拖拽
- 不支持待办分组
- 不修改完成/删除逻辑

## Decisions

### 添加 UI

**决定**：将输入框区域替换为「添加待办」按钮，点击后弹出 modal（`#todo-modal`），复用 `#bm-modal` 的样式和结构。

**理由**：与书签添加体验一致，容纳两个字段（标题+链接），结构复用减少重复代码。

### 编辑 UI

**决定**：待办 item 悬浮时显示编辑按钮（左上角，复用 `.bm-edit` 样式），点击预填 modal 并切换为编辑模式，模式标记用 `editingId`（与 Bookmarks 同模式）。

**理由**：与书签编辑体验一致。

### 链接展示

**决定**：`makeItem` 中判断 `t.url`，有值则渲染 `<a href target="_blank">`，无值渲染 `<span>`。

**理由**：最简单，不需要额外 CSS class 控制。

### 拖拽排序

**决定**：仅对未完成列表（`#todos-pending`）启用 HTML5 DnD，实现方式与书签拖拽完全一致：`dragstart` 记录 id，`dragover` 实时插入 DOM，`drop` 后 `rebuildPendingFromDOM()` 重建数组顺序。已完成列表不参与拖拽。

**理由**：已完成待办按完成时间排序更自然，不需要手动排序。

### 数据结构

新增字段 `url?: string`，旧数据无此字段视为无链接，完全向后兼容。

## Risks / Trade-offs

- [低] modal 替换输入框后快速添加体验略有下降（需多一步点击）→ 可接受，链接字段是用户明确需求
- [低] 拖拽与悬浮编辑按钮同时出现，需确保拖拽不触发编辑点击 → 编辑按钮用 `stopPropagation`，无冲突
