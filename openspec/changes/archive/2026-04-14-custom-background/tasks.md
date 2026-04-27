## 1. 数据模型与初始化

- [x] 1.1 在 `DEFAULT_CONFIG` 中新增 `settings: { backgroundImage: null }` 字段
- [x] 1.2 在 `Storage.init()` 迁移逻辑中，为旧配置补充缺失的 `settings` 字段（向后兼容）

## 2. DOM 结构

- [x] 2.1 在工具栏「导入」按钮右侧添加「设置」按钮（`#settings-btn`）
- [x] 2.2 在工具栏下方添加背景配置面板 `#bg-panel`（初始隐藏），包含「选择背景图」文件输入和「移除背景」按钮
- [x] 2.3 添加隐藏的 `<input type="file" id="bg-file" accept="image/*">` 用于触发文件选择

## 3. CSS 样式

- [x] 3.1 为 `body::before` 添加半透明遮罩伪元素样式（`position: fixed; inset: 0; background: rgba(0,0,0,0.55); pointer-events: none; z-index: 0`），默认隐藏（`content: none`）
- [x] 3.2 添加 `body.has-bg` 类样式：启用 `::before` 遮罩（`content: ''`），设置 `background-size: cover; background-position: center; background-attachment: fixed`
- [x] 3.3 为背景配置面板 `#bg-panel` 添加样式（与工具栏风格一致的行布局，收起时 `display:none`）
- [x] 3.4 确保 `#main-grid`、`#search-section`、`#toolbar` 等主要容器 `position` 相对于遮罩层在上方（`position: relative; z-index: 1`）

## 4. 背景图功能逻辑

- [x] 4.1 实现 `Background.apply(base64)` 函数：设置 `document.body.style.backgroundImage`，添加 `has-bg` class
- [x] 4.2 实现 `Background.remove()` 函数：清除 `backgroundImage` style，移除 `has-bg` class
- [x] 4.3 实现 `Background.init(cfg)` 函数：页面加载时若 `cfg.settings.backgroundImage` 非空则调用 `apply()`
- [x] 4.4 为「设置」按钮绑定点击事件：切换 `#bg-panel` 的显示/隐藏
- [x] 4.5 为「选择背景图」绑定点击事件，触发 `#bg-file` 的 `click()`
- [x] 4.6 为 `#bg-file` 绑定 `change` 事件：读取文件 → `FileReader.readAsDataURL()` → 写入 `cfg.settings.backgroundImage` → `Storage.save()` → `Background.apply()` → 收起面板；捕获 `QuotaExceededError` 并 alert 提示
- [x] 4.7 为「移除背景」按钮绑定点击事件：置 `cfg.settings.backgroundImage = null` → `Storage.save()` → `Background.remove()` → 收起面板
- [x] 4.8 根据 `cfg.settings.backgroundImage` 是否为空，初始化「移除背景」按钮的禁用状态；每次背景变更后同步更新禁用状态

## 5. 启动集成

- [x] 5.1 在 Boot 区域调用 `Background.init(config)`
