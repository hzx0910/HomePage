## 1. 数据模型与迁移

- [x] 1.1 在 `DEFAULT_CONFIG.settings` 中新增 `accentColor: '#6366f1'` 和 `showTodos: true` 字段
- [x] 1.2 在 `Storage.init()` 迁移逻辑中，为旧配置补填缺失的 `accentColor` 和 `showTodos` 字段

## 2. CSS 准备

- [x] 2.1 将 `:root` 中的 `--accent` / `--accent-hover` 改为通过 `--accent-rgb` 驱动，`body.has-bg` 中的 accent 覆盖也改用 `rgba(var(--accent-rgb), 0.75)` 形式，解耦主题色切换与半透明覆盖
- [x] 2.2 新增 `body.hide-todos #main-grid` 规则：`grid-template-columns: 1fr`
- [x] 2.3 新增 `body.hide-todos #todos-card` 规则：`display: none`

## 3. 移除旧内联面板

- [x] 3.1 删除 HTML 中的 `#bg-panel` 及其两个按钮（`#bg-choose-btn`、`#bg-remove-btn`）
- [x] 3.2 删除 CSS 中 `#bg-panel` 相关样式
- [x] 3.3 删除 `Background.init()` 中绑定 `#settings-btn` 切换面板、`#bg-choose-btn`、`#bg-remove-btn` 的事件代码

## 4. 设置弹窗 DOM

- [x] 4.1 新增设置弹窗 HTML：`.modal-backdrop#settings-modal`，内含 `.modal`，标题「设置」+ 关闭按钮
- [x] 4.2 弹窗内新增「背景图」分区：「选择背景图」按钮 + 「移除背景」按钮（复用原有逻辑）
- [x] 4.3 弹窗内新增「主题色」分区：6 个颜色色板 `<button class="color-swatch" data-color="..." data-rgb="...">` 排列展示
- [x] 4.4 弹窗内新增「待办区域」分区：一个 toggle 开关（`<input type="checkbox" id="todos-toggle">`）+ 标签

## 5. 设置弹窗 CSS

- [x] 5.1 新增 `.color-swatch` 样式：圆形色块，hover 缩放，选中状态显示勾选（`::after` 白色勾）
- [x] 5.2 新增设置分区标题 `.settings-section-title` 样式（与 `.card-title` 风格一致）
- [x] 5.3 新增 toggle 开关样式（纯 CSS，利用 `<input type="checkbox">` + `<label>` 实现滑动开关外观）

## 6. Settings 模块逻辑

- [x] 6.1 实现 `Settings.init(cfg)`：绑定 `#settings-btn` 点击打开弹窗；绑定遮罩和关闭按钮关闭弹窗
- [x] 6.2 实现 `Settings.applyAccent(color, rgb)`：`documentElement.style.setProperty('--accent', color)` + `--accent-hover`（亮色）+ `--accent-rgb`
- [x] 6.3 在 `Settings.init()` 中绑定色板点击事件：更新 `cfg.settings.accentColor` → `Storage.save()` → `applyAccent()` → 更新色板选中状态
- [x] 6.4 在 `Settings.init()` 中绑定待办 toggle 事件：更新 `cfg.settings.showTodos` → `Storage.save()` → 切换 `body.hide-todos` class
- [x] 6.5 在 `Settings.init()` 中绑定「选择背景图」和「移除背景」按钮（迁移自 `Background.init()`）
- [x] 6.6 实现 `Settings.restore(cfg)`：页面加载时根据 `cfg.settings` 恢复主题色、待办显示状态、色板选中状态、移除按钮禁用状态

## 7. 启动集成

- [x] 7.1 在 Boot 区域新增 `Settings.init(config)` 调用，移除 `Background.init(config)` 调用（逻辑已迁入 Settings）
