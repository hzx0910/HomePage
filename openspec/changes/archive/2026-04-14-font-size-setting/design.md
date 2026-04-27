## Context

页面当前使用固定的 `font-size: 14px` 作为 `body` 基准字号，所有文字大小均以 `em`/`rem` 或 `px` 固定书写。需要在不修改每处文字大小定义的前提下，实现全局字号的统一缩放。

## Goals / Non-Goals

**Goals:**
- 在设置弹窗中新增字体大小行，5 档调节（1–5，默认 3）
- 用户切换后全页文字立即同步缩放
- 配置持久化，刷新后恢复

**Non-Goals:**
- 不针对单个组件独立设置字号
- 不支持自定义任意数值

## Decisions

### CSS 变量驱动缩放

在 `:root` 中定义 `--font-scale: 1`，`body` 的 `font-size` 改为 `calc(14px * var(--font-scale))`。页面中已有的 `px` 字号改为相对 `body` 字号的 `em`，从而跟随缩放；已使用 `em`/`rem` 的部分自然继承。

5 档对应的 scale 值：
| 档位 | scale | 等效 body font-size |
|------|-------|---------------------|
| 1    | 0.857 | 12px                |
| 2    | 0.929 | 13px                |
| 3    | 1.000 | 14px（默认）         |
| 4    | 1.071 | 15px                |
| 5    | 1.143 | 16px                |

**选择 CSS 变量而非直接操作 body font-size**：与现有 `--accent-rgb` 等变量体系一致，JS 只需一行 `setProperty` 即可，无需遍历 DOM。

### 档位选择 UI

使用 5 个 `<button>` 排成一行（类似色板行），显示 "小 · 中小 · 中 · 中大 · 大" 标签，点击后高亮选中态。不使用 `<input type="range">` 避免样式适配复杂度。

### 配置存储

`settings.fontSize`（number，1–5）。旧配置无此字段时补填默认值 3。

## Risks / Trade-offs

- 现有 `px` 硬编码字号（如 `font-size: 12px`）不会随 `body font-size` 缩放，需逐一改为 `em`。遗漏项仅影响视觉一致性，不影响功能。
- scale 值精确到小数点后 3 位，浏览器渲染时可能产生亚像素差异，属可接受范围。
