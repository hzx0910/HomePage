## 1. 拆分 hide() 方法

- [x] 1.1 在 `Suggestions` 对象中新增 `hideOnly()` 方法：仅移除 `visible` class、重置 `_activeIndex`，不清空 `_items` 也不清空 DOM
- [x] 1.2 将 `blur` 事件中的 `Suggestions.hide()` 改为 `Suggestions.hideOnly()`

## 2. focus 时恢复联想词

- [x] 2.1 在 `input` 的事件绑定区域新增 `focus` 事件监听：若 `Suggestions._items.length > 0` 则调用 `Suggestions.render(Suggestions._items)` 重新显示
