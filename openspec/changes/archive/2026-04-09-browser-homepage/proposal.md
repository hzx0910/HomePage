## Why

需要一个个性化浏览器首页，替代默认的新标签页，提供搜索、书签和待办事项三合一的高效入口，减少日常工作流中的切换摩擦。

## What Changes

- 新增 `index.html` 作为浏览器首页入口，纯静态单文件
- 新增搜索框模块，支持快捷词切换搜索引擎
- 新增书签模块，支持分组管理和 favicon 显示
- 新增待办事项模块，支持简单勾选和完成记录
- 新增统一配置管理，所有数据通过 localStorage 以 JSON 格式持久化
- 新增配置导入/导出功能，方便跨设备迁移

## Capabilities

### New Capabilities

- `search`: 搜索框，支持多搜索引擎切换和快捷词（如 `g xxx`）
- `bookmarks`: 书签管理，支持分组、favicon、增删改
- `todos`: 待办事项，支持勾选完成、保留历史记录
- `config-storage`: 统一配置存储层，基于 localStorage，支持 JSON 导入/导出

### Modified Capabilities

## Impact

- 纯前端，无后端依赖
- 本地 `file://` 协议访问，无需服务器
- 所有数据存储在浏览器 localStorage，不涉及网络请求（搜索跳转除外）
