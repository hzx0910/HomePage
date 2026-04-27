## 1. 渲染层准备

- [x] 1.1 书签 item 渲染时添加 `draggable="true"` 属性和 `data-id` 属性（值为书签 id）
- [x] 1.2 分组容器 `.bm-group-items` 渲染时添加 `data-group` 属性（值为分组名称）

## 2. 拖拽事件绑定

- [x] 2.1 书签 item 绑定 `dragstart` 事件：记录被拖拽书签的 id 到 `dragState`
- [x] 2.2 书签 item 绑定 `dragover` 事件：`preventDefault()` 允许放置，添加视觉反馈 class
- [x] 2.3 书签 item 绑定 `drop` 事件：将拖拽书签插入到目标书签之前，更新分组并保存
- [x] 2.4 分组容器 `.bm-group-items` 绑定 `dragover` 和 `drop` 事件：支持拖入空分组或分组末尾

## 3. 数据更新与持久化

- [x] 3.1 实现 `rebuildFromDOM()` 方法：从当前 DOM 中读取各分组的书签顺序和分组归属，重建 `cfg.bookmarks` 数组
- [x] 3.2 drop 事件结束后调用 `rebuildFromDOM()`，保存到 localStorage 并重新渲染

## 4. CSS 视觉反馈

- [x] 4.1 添加 `.drag-over` 样式：书签 item 被悬停时显示高亮边框，提示可放置位置
