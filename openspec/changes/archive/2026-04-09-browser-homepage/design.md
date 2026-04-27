## Context

项目从零开始，无历史代码。目标是一个本地使用的浏览器首页，通过 `file://` 协议直接打开 `index.html`，无需任何构建工具或服务器。

## Goals / Non-Goals

**Goals:**
- 单 HTML 文件，内联 CSS 和 JS，零外部依赖
- 搜索框支持多搜索引擎和快捷词
- 书签支持分组和 favicon
- 待办支持勾选和历史保留
- 所有数据用 localStorage 持久化，JSON 格式
- 支持配置整体导出/导入

**Non-Goals:**
- 多用户/账号同步
- 云端存储
- PWA/Service Worker
- 移动端适配

## Decisions

### 单文件架构

**决定**：将 HTML、CSS、JS 全部内联在 `index.html` 中。

**理由**：`file://` 协议下加载外部 CSS/JS 文件在某些浏览器有限制，单文件最简单可靠，也方便直接分发和备份。

### 数据结构

**决定**：所有数据存在 localStorage 的单一 key `homepage_config` 下，JSON 格式：

```json
{
  "version": 1,
  "search": {
    "defaultEngine": "google",
    "engines": [
      { "name": "google", "prefix": "g", "url": "https://www.google.com/search?q={q}" },
      { "name": "github", "prefix": "gh", "url": "https://github.com/search?q={q}" }
    ]
  },
  "bookmarks": [
    {
      "id": "uuid",
      "group": "常用",
      "title": "GitHub",
      "url": "https://github.com",
      "favicon": ""
    }
  ],
  "todos": [
    {
      "id": "uuid",
      "text": "任务内容",
      "done": false,
      "createdAt": "ISO8601",
      "doneAt": null
    }
  ]
}
```

**理由**：单一配置对象便于整体导出/导入迁移，版本字段为未来格式升级预留空间。

### Favicon 获取

**决定**：使用 Google Favicon 服务 `https://www.google.com/s2/favicons?domain=<domain>` 自动获取 favicon。

**理由**：无需本地存储图片，简单可靠。用户离线时显示默认图标降级。

### UI 风格

**决定**：极简暗色主题，卡片式布局。

**理由**：作为每天使用的首页，视觉干扰应尽量少。

## Risks / Trade-offs

- [localStorage 容量限制约 5MB] → 书签和待办数量多时可能超限。缓解：定期提示用户清理已完成待办；favicon 不缓存到 localStorage
- [file:// 协议下 favicon 请求] → 发起外部 HTTP 请求是正常的，搜索跳转同理，不影响核心功能
- [无版本迁移机制] → 通过 `version` 字段预留，首版暂不实现迁移逻辑
