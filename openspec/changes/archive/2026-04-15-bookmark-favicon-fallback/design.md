## Context

当前代码路径：
1. 有 favicon URL → `img.src = favUrl; img.onerror = () => { img.style.display = 'none'; }`
2. 无 favicon URL → `img.style.display = 'none'`

两条路径最终都把图标区域隐藏。`.bm-item img` 宽高 14px。

## Goals / Non-Goals

**Goals:**
- favicon 失败时展示 14×14px 的主题色圆角矩形 + 首字符
- 图标颜色跟随主题色（`--accent`）实时变化

**Non-Goals:**
- 不预加载/缓存 favicon
- 不修改 favicon 请求逻辑
- 不处理标题为空的极端情况（显示空白即可）

## Decisions

### 方案：内联 SVG data URL 作为 img.src 替换

生成一个 SVG 字符串，以 `data:image/svg+xml,...` 格式赋给 `img.src`。

**优点：**
- 纯字符串，无额外 DOM 元素
- 无需改动 CSS（复用现有 `.bm-item img` 样式）
- 可读取 CSS 变量 `--accent` 实时生成

**SVG 结构：**
```svg
<svg xmlns="..." width="14" height="14" viewBox="0 0 14 14">
  <rect width="14" height="14" rx="3" fill="<accent-color>"/>
  <text x="7" y="10.5" font-size="9" font-family="sans-serif"
        fill="white" text-anchor="middle" dominant-baseline="auto">A</text>
</svg>
```
- `rx="3"` 对应圆角矩形
- 字符取 `bm.title` 的第一个字符（`[...bm.title][0]` 处理 emoji/CJK）
- accent 颜色通过 `getComputedStyle(document.documentElement).getPropertyValue('--accent').trim()` 读取

### 辅助函数：`Bookmarks.faviconFallback(title)`

```js
faviconFallback(title) {
  const char = ([...title][0] || '?').toUpperCase();
  const color = getComputedStyle(document.documentElement)
    .getPropertyValue('--accent').trim();
  const svg = `<svg xmlns="http://www.w3.org/2000/svg" width="14" height="14" viewBox="0 0 14 14">
    <rect width="14" height="14" rx="3" fill="${color}"/>
    <text x="7" y="10.5" font-size="9" font-family="sans-serif" fill="white" text-anchor="middle">${char}</text>
  </svg>`;
  return `data:image/svg+xml,${encodeURIComponent(svg)}`;
},
```

在 `onerror` 和无 URL 两处调用此函数替换 `img.src`，并确保 `img.style.display` 不为 `none`。

## Risks / Trade-offs

- `getComputedStyle` 读取的是当前主题色，但主题切换后已渲染的 fallback 图标不会自动更新（需要重新 render）。由于主题切换会触发 `Bookmarks.render()` 重新渲染，所以图标会随之更新，无问题。
- SVG 中 `fill` 若使用 `var(--accent)` 字符串无法直接工作（SVG data URL 中 CSS 变量不解析），因此需要读取计算值。
