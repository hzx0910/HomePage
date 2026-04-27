## Why

书签顺序固定，用户无法调整常用书签的位置，也不能将书签从一个分组移动到另一个分组。支持拖拽排序后，用户可以自由整理书签布局，提升日常使用效率。

## What Changes

- 书签支持拖拽排序：在同一分组内拖动可调整顺序
- 书签支持跨分组拖动：拖动到另一个分组后归入该分组
- 排序结果持久化到 localStorage

## Capabilities

### New Capabilities

（无）

### Modified Capabilities

- `bookmarks`：书签新增拖拽排序与跨分组移动能力

## Impact

- 修改 `index.html` 书签渲染逻辑（为书签 item 添加 draggable 属性及拖拽事件）
- 新增分组容器的拖拽放置区域逻辑
- 保存逻辑需在拖拽结束后更新 localStorage 中书签顺序
