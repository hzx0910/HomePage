## Why

当前搜索框只有一个通用搜索按钮，每次使用不同搜索引擎需要手动输入快捷词，不够直观。改为三个固定搜索引擎按钮（百度、Bing、Google），让用户一眼看清并一键选择目标引擎，同时保留默认引擎偏好的本地缓存。

## What Changes

- **BREAKING** 移除原有的单一"搜索"按钮，替换为三个搜索引擎按钮（百度、Bing、Google）
- 每个按钮独立触发对应搜索引擎的搜索
- 三个按钮中有一个标记为"默认"，按 Enter 键使用默认引擎搜索
- 用户可通过按钮上的标记切换默认搜索引擎，切换结果持久化到 localStorage
- 保留快捷词机制（`g`/`b`/`bd` 等前缀）作为补充

## Capabilities

### New Capabilities

（无新能力，均为对现有搜索能力的修改）

### Modified Capabilities

- `search`：UI 从单按钮改为三按钮，新增默认引擎切换交互和持久化逻辑

## Impact

- 修改 `index.html` 中搜索区域的 HTML 结构和 CSS
- 修改 `Search` JS 模块：多按钮事件绑定、默认引擎切换、localStorage 读写
- 修改 `homepage_config` 中 `search.defaultEngine` 的写入时机（由初始化时一次性设置改为用户操作时实时更新）
