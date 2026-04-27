## 1. HTML 结构

- [x] 1.1 用 `<div class="search-input-wrap">` 包裹 `#search-input`
- [x] 1.2 在 wrap 内插入清空按钮 `<button id="search-clear">×</button>`

## 2. CSS 样式

- [x] 2.1 `.search-input-wrap` 设为 `position: relative; flex: 1`
- [x] 2.2 `#search-input` 加足够 `padding-right`（为清空按钮留空间）
- [x] 2.3 `#search-clear` 绝对定位在输入框内右侧，圆形样式，默认 `opacity: 0; pointer-events: none`
- [x] 2.4 `.search-input-wrap.has-value #search-clear` 设为 `opacity: 1; pointer-events: auto`

## 3. JS 逻辑

- [x] 3.1 监听 `#search-input` 的 `input` 事件，有内容时给 wrap 加 `.has-value`，无内容时移除
- [x] 3.2 监听 `#search-clear` 点击事件：清空输入框、移除 `.has-value`、将焦点回到输入框
