## Why

`color-mix(in srgb, ...)` CSS 函数在 Windows Chrome 通过 `file://` 协议打开页面时无法正确渲染，导致 `--surface`、`--surface2`、`--border`、`--modal-bg` 四个关键 CSS 变量失效，模块背景和边框完全透明，页面不可用。需要用纯 JS 线性混色替代，同时保证颜色值和透明度与原 `color-mix()` 计算结果**精确一致**。

## What Changes

- CSS `:root` 中四个 `color-mix()` 变量替换为等价静态值（作为 JS 执行前的 fallback）
- JS `Settings.applyAccent()` 中增加线性混色计算，动态设置这四个变量，颜色和 alpha 与原 `color-mix()` 精确一致
- `body.has-bg` CSS 规则中移除 `color-mix()` 覆盖行
- `_applyBackground()` 和 `_removeBackground()` 在操作背景后调用 `applyAccent()` 联动更新 surface 透明度

## Capabilities

### New Capabilities

- `accent-derived-colors`: JS 驱动的派生颜色计算，精确还原 `color-mix()` 的 RGB 和 alpha 结果，兼容 Windows Chrome `file://` 协议

### Modified Capabilities

- `custom-background`: 背景图应用/移除时联动更新 surface 颜色透明度

## Impact

- `index.html` CSS `:root` 四个变量定义
- `index.html` `body.has-bg` CSS 规则
- `index.html` JS `Settings.applyAccent()`、`_applyBackground()`、`_removeBackground()`
