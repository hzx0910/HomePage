## Context

CSS `color-mix(in srgb, A p%, B)` 的精确等价计算：
- RGB 通道：`result = round(B * (1-p) + A * p)`
- alpha 通道：`result_alpha = A_alpha * p + B_alpha * (1-p)`

默认主题色 `rgb(30,58,110)` 下各变量的精确计算结果：

| 变量 | 原定义 | 等价值 |
|---|---|---|
| `--surface` | `color-mix(in srgb, accent 12%, #13151f)` | `rgba(20,25,40,1)` |
| `--surface2` | `color-mix(in srgb, accent 16%, #191c2e)` | `rgba(26,33,56,1)` |
| `--border` | `color-mix(in srgb, accent 22%, rgba(30,34,56,0.4))` | `rgba(30,39,68,0.532)` |
| `--modal-bg` | `color-mix(in srgb, accent 14%, rgba(13,15,23,0.85))` | `rgba(15,21,35,0.871)` |

`--border` alpha 计算：`0.22×1 + 0.78×0.4 = 0.532`  
`--modal-bg` alpha 计算：`0.14×1 + 0.86×0.85 = 0.871`

## Goals / Non-Goals

**Goals:**
- 精确还原 `color-mix()` 的颜色和透明度（视觉无差异）
- 消除对 `color-mix()` 的依赖，兼容 Windows Chrome `file://`
- 切换主题色时派生颜色同步更新
- 有背景图时 surface 半透明，无背景图时不透明

**Non-Goals:**
- 不改变功能逻辑或数据结构
- 不处理 IE/旧 Edge

## Decisions

### 决策 1：JS 线性插值精确还原 color-mix

在 `applyAccent(color, rgb, hoverRgb)` 中：
1. 解析 `rgb` 字符串为 `[r, g, b]`
2. 用 `mix(base, accent, t) = round(base*(1-t) + accent*t)` 计算 RGB 通道
3. 用 `baseAlpha*(1-t) + 1*t` 计算 alpha 通道（accent alpha 始终为 1）
4. 输出 `rgba(r,g,b,a)` 字符串，通过 `style.setProperty` 写入 CSS 变量

### 决策 2：has-bg 时 surface alpha 降为 0.3

原 `has-bg` 规则中 `color-mix(in srgb, accent 12%, rgba(19,21,31,0.3))` 的 base alpha 为 0.3，因此有背景图时 surface alpha = `0.12×1 + 0.88×0.3 = 0.384`，约 `0.38`。

`applyAccent()` 检测 `body.has-bg` 类，有背景图时 surface/surface2 使用 alpha `0.38`，无背景图时使用 `1`。

### 决策 3：CSS fallback 使用默认主题色的精确计算值

`:root` 中直接写入默认主题色的计算结果，JS 执行后立即覆盖为当前主题色的值。

## Risks / Trade-offs

- [风险] 浮点精度：alpha 值保留 3 位小数，视觉差异可忽略 → 可接受
- [风险] 多处调用 `applyAccent()`：只在用户交互时触发，无性能问题
