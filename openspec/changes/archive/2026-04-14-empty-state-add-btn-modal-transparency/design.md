## Context

当前书签空态显示 `.empty-hint`（纯文字「暂无书签」），没有操作入口。弹窗背景使用 `--modal-bg: color-mix(in srgb, var(--accent) 14%, rgba(13,15,23,0.95))`，alpha 为 0.95，视觉上接近不透明。搜索推荐词区域使用 `rgba(26, 29, 39, 0.95)` 同样是 0.95 alpha。两者数值相近但色调不同，且在背景图存在时均显示偏厚重。

## Goals / Non-Goals

**Goals:**
- 书签空态替换为可操作的「＋ 添加书签」按钮，样式参考 `.bm-inline-add`
- 弹窗透明度与搜索推荐词区域视觉一致，且仍随主题色变化

**Non-Goals:**
- 不改变待办空态（「暂无待办」保留，待办有独立的内联添加按钮）
- 不修改添加书签/添加备忘弹窗的字段或交互逻辑
- 不改变搜索推荐词区域的背景值

## Decisions

### 书签空态：`.bm-empty-add` 按钮替换 `.empty-hint`

在 `Bookmarks.render()` 中，当 `bookmarks.length === 0` 时，不再 render `<div class="empty-hint">暂无书签</div>`，而是 render 一个 `<button class="bm-empty-add">＋ 添加书签</button>`，点击触发 `this.openModal()`。样式参考 `.bm-inline-add`（虚线边框、主题色），但宽度拉伸填满容器，更具空态引导感。

### 弹窗透明度：统一使用 `--modal-bg` 并降低 alpha

当前 `--modal-bg` 的 base 颜色 alpha 为 0.95，视觉上偏厚。改为 `rgba(13,15,23,0.85)` 作为 base（alpha 降至 0.85），让背景图/环境光透出来，与搜索推荐词区域的视觉感受接近。`color-mix` 的 accent 比例保持 14% 不变，保证主题联动。

最终值：`--modal-bg: color-mix(in srgb, var(--accent) 14%, rgba(13,15,23,0.85))`

> **为什么不直接用 `rgba(26,29,39,0.95)` 对齐搜索推荐词？** 搜索推荐词背景是硬编码值不随主题变化，而弹窗上一版已要求随主题切换，直接使用硬编码值会回退该需求。降低 alpha 既保留主题联动，又达到透明感。

## Risks / Trade-offs

- 降低 alpha 后，在纯黑背景（无背景图）下弹窗背景稍微偏灰，可接受
- `.bm-empty-add` 按钮在极窄屏上可能超出卡片宽度，设置 `max-width: 100%` 即可
