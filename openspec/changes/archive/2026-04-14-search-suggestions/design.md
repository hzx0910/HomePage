## Context

项目为纯静态单文件 HTML，直接通过 `file://` 协议在浏览器中打开，无服务器环境。搜索框已存在，默认搜索引擎存储在 `localStorage` 的 `settings` 对象中。需在不引入构建工具和外部框架的前提下，接入搜索引擎的联想词 API。

由于 `file://` 协议的跨域限制，无法直接发起 `fetch` 请求到外部 API，需使用 JSONP 或浏览器扩展豁免策略。

## Goals / Non-Goals

**Goals:**
- 输入时实时获取并展示联想词（防抖，减少请求频率）
- 支持鼠标点击和键盘（↑↓ / Enter / Esc）交互
- 自动适配当前默认搜索引擎（Google / 百度 / Bing）
- 纯前端实现，无需后端代理

**Non-Goals:**
- 不缓存联想词到 localStorage
- 不支持自定义联想词来源
- 不实现联想词高亮匹配

## Decisions

### 决策 1：使用 JSONP 而非 fetch

**选择**：JSONP

**理由**：项目通过 `file://` 协议运行，浏览器会阻止跨域 `fetch` 请求。JSONP 通过动态插入 `<script>` 标签绕过此限制，各主流搜索引擎的 Suggestions API 均支持 JSONP 回调。

**备选方案**：fetch + CORS — 在 `file://` 协议下不可行；浏览器插件代理 — 侵入性太强，不在本项目范围内。

各引擎 JSONP endpoint：
- **Google**: `https://suggestqueries.google.com/complete/search?client=firefox&q=<keyword>&callback=<fn>`
- **百度**: `https://suggestion.baidu.com/su?wd=<keyword>&cb=<fn>`
- **Bing**: `https://api.bing.com/qsonhs.aspx?type=cb&q=<keyword>&cb=<fn>`

### 决策 2：防抖延迟 300ms

**理由**：平衡响应速度与请求频率，避免每次按键都发出请求。300ms 是业界常用值，适合搜索联想场景。

### 决策 3：联想词列表作为独立 DOM 元素（绝对定位）

**理由**：列表需要覆盖在页面其他内容上方，使用绝对定位 + z-index 控制层级，宽度与搜索框对齐。不修改现有布局结构，降低回归风险。

### 决策 4：每次请求生成唯一回调函数名

**理由**：避免并发 JSONP 请求之间的回调冲突，请求完成后立即清理 `window` 上的回调函数和 `<script>` 标签。

## Risks / Trade-offs

- **JSONP 安全性** → 仅用于只读的搜索联想词，不涉及用户凭据，风险可接受
- **API 可用性** → 第三方免费 API 可能限流或下线，加入 try/catch，失败时静默不展示
- **Google API 国内访问** → 国内用户可能无法访问 Google Suggestions，但用户若将默认引擎设为百度/Bing 则无影响
- **脚本标签累积** → 每次 JSONP 调用后立即移除 `<script>` 标签，防止 DOM 污染

## Migration Plan

纯前端新增功能，无数据迁移。直接更新 `index.html` 即可，旧用户刷新页面后自动生效。
