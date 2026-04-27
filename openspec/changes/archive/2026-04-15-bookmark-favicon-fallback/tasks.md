## 1. 辅助函数

- [x] 1.1 在 `Bookmarks` 对象中新增 `faviconFallback(title)` 方法：读取 `--accent` 计算值，生成含圆角矩形背景和首字符的内联 SVG data URL

## 2. 降级逻辑替换

- [x] 2.1 将 `img.onerror` 回调从 `img.style.display = 'none'` 改为调用 `faviconFallback(bm.title)` 赋给 `img.src`（同时确保 `img.style.display` 不设为 none）
- [x] 2.2 将无法生成 favicon URL 时的 `img.style.display = 'none'` 改为直接设置 `img.src = this.faviconFallback(bm.title)`
