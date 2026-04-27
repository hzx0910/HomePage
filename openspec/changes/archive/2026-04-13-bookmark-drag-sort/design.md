## Context

书签渲染使用 JS 动态生成 DOM：`cfg.bookmarks` 数组按 `group` 字段分组，每组渲染一个 `.bm-group-items` 容器，容器内每个书签是一个 `<a class="bm-item">` 元素。数据顺序即渲染顺序。

项目为纯静态单文件，不引入任何外部库。

## Goals / Non-Goals

**Goals:**
- 书签 item 可在同一分组内拖拽排序
- 书签可跨分组拖拽，拖入目标分组后归入该分组
- 拖拽结束后立即持久化到 localStorage

**Non-Goals:**
- 不支持分组本身的拖拽排序
- 不做拖拽动画/占位符预览（保持实现简单）
- 不引入第三方拖拽库

## Decisions

### 拖拽实现方式

**决定**：使用原生 HTML5 Drag and Drop API（`draggable="true"` + `dragstart` / `dragover` / `drop` 事件）。

**理由**：项目纯静态不用框架，不引入外部库。HTML5 DnD 已足够实现基本排序，无额外依赖。

**方案对比**：
- Sortable.js 等库：功能丰富但引入外部依赖，与项目约束冲突
- 鼠标事件（mousedown/mousemove）：需自行处理位置计算，复杂度高
- HTML5 DnD ✓：原生支持，实现简洁

### 数据更新策略

**决定**：拖拽结束（`drop` 事件）后，从 DOM 顺序重建 `cfg.bookmarks` 数组，更新每个书签的 `group` 字段（跨组时），然后保存到 localStorage 并重新渲染。

**理由**：DOM 已是唯一真实顺序来源，从 DOM 反推数据最简单可靠，避免维护两份状态。

### 拖拽目标范围

**决定**：`.bm-group-items` 容器作为 drop zone，书签 item 本身也接受 drop（插入到该 item 之前）。

**理由**：支持精确插入位置，用户体验更好。

## Risks / Trade-offs

- [中] HTML5 DnD 在移动端支持有限 → 项目定位为桌面浏览器首页，可接受
- [低] 从 DOM 重建数组依赖 `data-id` 属性标记每个书签 item → 渲染时需确保每个 `.bm-item` 带有 `data-id`
