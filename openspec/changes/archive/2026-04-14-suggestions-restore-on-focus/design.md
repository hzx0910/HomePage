## Context

当前 `Suggestions.hide()` 同时做两件事：清空 `_items`、移除 DOM 内容、移除 `visible` class。`blur` 事件直接调用此方法，导致缓存丢失。重新 focus 时无数据可恢复，需重新输入触发 `input` 事件才能拉取联想词。

## Goals / Non-Goals

**Goals:**
- blur 时保留 `_items` 缓存，只隐藏 UI
- focus 时若有缓存自动重新渲染
- 搜索成功、清空输入、Escape 键时完全清空缓存

**Non-Goals:**
- 不改变联想词的拉取逻辑（debounce、JSONP）
- 不改变键盘导航行为

## Decisions

### 拆分 hide() 为两个方法

- **`hideOnly()`**：仅视觉隐藏，`list.classList.remove('visible')` + 重置 `_activeIndex`，保留 `_items`
- **`hide()`**：完全清空，清空 `_items`、清空 DOM、移除 `visible` class（现有调用方行为不变）

`blur` 事件改为调用 `hideOnly()`。

### focus 事件：有缓存时重新渲染

```js
input.addEventListener('focus', () => {
  if (Suggestions._items.length) Suggestions.render(Suggestions._items);
});
```

直接复用 `render()` 方法，无需新增逻辑。

### 调用方梳理

| 调用位置 | 当前方法 | 改后 |
|---|---|---|
| `blur` 事件 | `hide()` | `hideOnly()` |
| 搜索执行后 | `hide()` | `hide()` 不变 |
| 清空按钮 | `hide()` | `hide()` 不变 |
| Escape 键 | `hide()` | `hide()` 不变 |
| 引擎切换后 | `hide()` | `hide()` 不变 |

## Risks / Trade-offs

- 若用户 blur 后输入框内容被外部清空（当前无此场景），focus 时可能显示与当前输入不匹配的联想词。当前页面无此场景，可忽略。
