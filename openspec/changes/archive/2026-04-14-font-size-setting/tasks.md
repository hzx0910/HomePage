## 1. 数据模型与迁移

- [x] 1.1 在 `DEFAULT_CONFIG.settings` 中新增 `fontSize: 3` 字段
- [x] 1.2 在 `Storage.init()` 迁移逻辑中，为旧配置补填缺失的 `fontSize` 字段（默认值 3）

## 2. CSS 准备

- [x] 2.1 在 `:root` 中新增 `--font-scale: 1` 变量
- [x] 2.2 将 `body` 的 `font-size` 改为 `calc(14px * var(--font-scale))`
- [x] 2.3 将页面中硬编码的 `px` 字号（如 `12px`、`13px` 等）改为 `em` 单位，使其跟随 body 字号缩放

## 3. 设置弹窗 DOM

- [x] 3.1 在设置弹窗中新增「字体大小」分区，包含标题和 5 个档位按钮（标签：小 / 中小 / 中 / 中大 / 大），按钮添加 `data-size="1~5"` 属性

## 4. 设置弹窗 CSS

- [x] 4.1 新增字体档位按钮 `.font-size-btn` 样式：与色板行风格一致，横排，选中态高亮（使用 `--accent` 颜色边框/背景）

## 5. Settings 模块逻辑

- [x] 5.1 实现 `Settings.applyFontSize(size)`：根据档位计算 scale（`[0.857, 0.929, 1, 1.071, 1.143][size-1]`），`documentElement.style.setProperty('--font-scale', scale)`
- [x] 5.2 在 `Settings.init()` 中绑定字体档位按钮点击事件：更新 `cfg.settings.fontSize` → `Storage.save()` → `applyFontSize()` → 更新按钮选中状态
- [x] 5.3 在 `Settings.restore(cfg)` 中恢复字体大小：调用 `applyFontSize()` 并同步按钮选中状态
