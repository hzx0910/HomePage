## 1. DOM 结构与样式

- [x] 1.1 在搜索框容器内添加联想词列表容器元素 `#suggestions-list`（绝对定位，z-index 置顶，初始隐藏）
- [x] 1.2 为联想词列表添加 CSS 样式：宽度对齐搜索框、背景色、圆角、阴影、滚动限高
- [x] 1.3 为联想词列表项 `.suggestion-item` 添加悬停高亮和键盘选中高亮样式

## 2. JSONP 请求封装

- [x] 2.1 实现 `fetchSuggestions(query, engine)` 函数，根据引擎名动态选择对应的 JSONP endpoint
- [x] 2.2 实现通用 JSONP 工具函数：生成唯一回调名、动态插入 `<script>` 标签、请求完成后清理标签和 `window` 属性
- [x] 2.3 实现超时处理（5s），超时后清理资源并静默失败

## 3. 联想词列表渲染

- [x] 3.1 实现 `renderSuggestions(items)` 函数，将联想词数组渲染为列表项并展示列表
- [x] 3.2 实现 `hideSuggestions()` 函数，隐藏列表并重置键盘高亮索引
- [x] 3.3 解析各搜索引擎 JSONP 响应格式，统一提取联想词字符串数组（Google/百度/Bing 格式各异）

## 4. 搜索框事件监听

- [x] 4.1 为搜索输入框绑定 `input` 事件，防抖 300ms 后调用 `fetchSuggestions`；输入为空时调用 `hideSuggestions`
- [x] 4.2 为搜索输入框绑定 `blur` 事件，延迟 150ms 后调用 `hideSuggestions`
- [x] 4.3 为搜索输入框绑定 `keydown` 事件，处理 ↑ / ↓ 导航（更新高亮项并回填搜索框）、Enter 确认（有高亮项时触发搜索）、Esc 关闭列表

## 5. 联想词点击交互

- [x] 5.1 为每个联想词列表项绑定 `mousedown` 事件（使用 mousedown 而非 click，避免被 blur 延迟干扰），触发默认引擎搜索并关闭列表

## 6. 搜索框行为修改

- [x] 6.1 修改引擎按钮点击处理器：搜索执行后调用 `hideSuggestions` 关闭列表
- [x] 6.2 修改 Enter 键处理逻辑：当联想词列表有键盘高亮项时，优先使用高亮项内容搜索，而非搜索框当前内容
