## Why

卡片标题行（「书签」标题 + ＋ 按钮、「待办」标题）占据了视觉空间却信息密度低，去掉后界面更简洁。同时将添加书签的入口内联到书签列表末尾，操作更直觉——就在内容旁边，无需寻找工具栏按钮。

## What Changes

- 隐藏书签卡片的 `.card-header`（「书签」标题行 + ＋ 按钮）
- 隐藏待办卡片的 `.card-header`（「待办」标题行）
- 在书签渲染完成后，于最后一个书签分组的书签行末尾追加一个「＋」内联添加按钮（`.bm-inline-add`）
- 点击该按钮触发与原来 `#bm-add-btn` 相同的添加书签弹窗逻辑
- 移除 `#bm-add-btn` 的点击事件绑定（或隐藏该按钮，因 card-header 整体隐藏后已不可见）

## Capabilities

### New Capabilities

- `bookmark-inline-add`: 书签列表末尾内联「添加」按钮，替代卡片标题栏中的 ＋ 按钮

### Modified Capabilities

- `bookmarks`: 书签卡片标题行隐藏，添加入口移至内联位置

## Impact

- `index.html`：隐藏两处 `.card-header` 的 CSS、新增 `.bm-inline-add` 样式、修改 `Bookmarks.render()` 在末尾插入内联添加按钮
