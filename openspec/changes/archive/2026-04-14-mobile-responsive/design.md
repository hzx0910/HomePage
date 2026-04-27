## Context

页面当前搜索区使用 `grid-template-columns: 3fr 1fr` 两列，主内容区使用 `grid-template-columns: 3fr 1fr` 两列，均为固定桌面布局，无任何媒体查询断点。在宽度 ≤ 600px 的设备上两列会被严重压缩。

## Goals / Non-Goals

**Goals:**
- 窄屏（≤ 600px）下搜索区和主内容区切换为单列堆叠布局
- 窄屏下引擎按钮移至搜索框下方（不再与搜索框并排）
- 窄屏下待办卡片堆叠到书签卡片下方
- 窄屏下收窄 body padding，避免内容贴边

**Non-Goals:**
- 不新增 JS，不改动 HTML 结构
- 不处理平板中等断点（600px–960px），保持两列布局
- 不针对各组件内部做像素级微调（字号、图标大小等）

## Decisions

### 断点值：600px

移动设备竖屏宽度通常为 360px–430px，600px 以下可安全视为手机。平板横屏（768px+）保持桌面双列布局。

### 纯 CSS `@media` 实现

当前布局完全基于 CSS Grid，通过 `@media (max-width: 600px)` 覆盖 `grid-template-columns` 即可，无需 JS 介入。与现有 `body.hide-todos` 纯 CSS 方案保持一致。

### 搜索区单列

窄屏时 `#search-form` 改为 `grid-template-columns: 1fr`，引擎按钮组自然堆叠到搜索框下方，行数变为两行。

### 主内容区单列

窄屏时 `#main-grid` 改为 `grid-template-columns: 1fr`，书签卡片在上，待办卡片在下。`body.hide-todos` 的 `1fr` 规则在窄屏下仍有效，无冲突。

## Risks / Trade-offs

- [引擎按钮区高度增加] → 在非常矮的屏幕（如横屏手机）上搜索区占屏比更大，可接受，用户主要竖屏使用
- [max-width 从 1200px 降为 100% 的窄屏处理] → 保持 `max-width: 1200px`，窄屏时自然被视口约束，无需额外修改
