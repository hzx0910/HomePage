## Why

待办区域当前宽度与书签区域等宽，占用了过多横向空间。缩小待办区域宽度，让页面布局更紧凑，视觉重心向书签倾斜。

## What Changes

- 待办区域宽度缩小为原来的一半（约 50%）

## Capabilities

### New Capabilities

（无）

### Modified Capabilities

- `todos`: 待办区域的显示宽度发生变化

## Impact

- 修改 `index.html` 中待办区域的 CSS 宽度/flex 属性
