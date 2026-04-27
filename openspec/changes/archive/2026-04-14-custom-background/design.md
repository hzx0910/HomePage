## Context

项目为纯静态单文件 HTML，通过 `file://` 或 HTTP 协议打开。所有数据存于 `localStorage`。当前 `homepage_config` 没有 `settings` 字段，背景固定为 CSS 变量 `--bg: #0f1117`。

## Goals / Non-Goals

**Goals:**
- 用户可选择本地图片作为全页背景，刷新后持久保留
- 背景图以遮罩保证内容可读性
- 可随时移除背景图恢复默认

**Non-Goals:**
- 不支持 URL 方式指定背景（跨域/CSP 复杂性）
- 不支持多张图片或幻灯片轮播
- 不支持背景色自定义（仅图片）

## Decisions

### 决策 1：Base64 存储于 localStorage

**选择**：`FileReader.readAsDataURL()` 转 Base64，写入 `homepage_config.settings.backgroundImage`

**理由**：无需服务器，与现有导入/导出机制完全兼容（JSON 一体化）。图片随配置文件整体迁移。

**备选**：IndexedDB — 支持大文件，但 API 复杂，且与现有 JSON 导出不兼容；`<input type=file>` + `URL.createObjectURL` — 仅页面生命周期内有效，刷新即失。

**限制**：典型壁纸 1–3MB，Base64 膨胀约 33%，localStorage 上限通常 5–10MB。提示用户选择文件大小合理的图片（建议 2MB 以内）；超限时捕获 `QuotaExceededError` 并提示。

### 决策 2：CSS `background` 作用于 `body`，叠加伪元素遮罩

**选择**：动态设置 `document.body.style.backgroundImage`，同时通过 `body::before` 伪元素添加半透明深色遮罩（`rgba(0,0,0,0.55)`）

**理由**：不影响现有布局，遮罩保证所有卡片和文字在任意背景下可读。不需要修改现有 DOM 结构。

### 决策 3：「设置」按钮放在工具栏「导入」按钮右侧

**理由**：与导入/导出功能语义相近，符合用户预期位置。UI 改动最小。

### 决策 4：设置面板为内联展开区域（非 modal）

**选择**：点击「设置」按钮在工具栏下方展开/收起一个配置区域，包含「选择背景图」和「移除背景」两个操作

**理由**：背景配置操作简单，不需要 modal 的遮罩层，减少视觉打扰。与页面整体轻量风格一致。

## Risks / Trade-offs

- **localStorage 配额超限** → 捕获 `QuotaExceededError`，提示用户选择更小的图片，不写入数据
- **导出 JSON 体积变大** → 含 Base64 图片的配置可能达数 MB，属预期行为，文档中说明
- **图片格式兼容性** → `<input accept="image/*">` 由浏览器处理，主流格式均支持

## Migration Plan

新增 `homepage_config.settings` 字段，默认值为 `{ backgroundImage: null }`。现有配置无此字段时，读取时视为 `null`，不影响现有功能。
