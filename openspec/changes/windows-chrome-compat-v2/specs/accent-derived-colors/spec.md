## ADDED Requirements

### Requirement: JS 精确还原 color-mix 派生颜色
系统 SHALL 在 `Settings.applyAccent()` 中通过 JS 线性插值计算 `--surface`、`--surface2`、`--border`、`--modal-bg`，结果与原 `color-mix(in srgb, ...)` 精确一致，包括 alpha 通道。

#### Scenario: 默认主题色下派生颜色值正确
- **WHEN** 页面以默认主题色（`#1e3a6e`，`rgb(30,58,110)`）加载
- **THEN** `--surface` 为 `rgba(20,25,40,1)`，`--surface2` 为 `rgba(26,33,56,1)`，`--border` alpha 约为 `0.532`，`--modal-bg` alpha 约为 `0.871`

#### Scenario: 切换主题色后派生颜色更新
- **WHEN** 用户切换到其他主题色
- **THEN** 四个派生变量立即更新为基于新主题色的混色结果，模块背景和边框颜色随之变化

#### Scenario: 无背景图时 surface 不透明
- **WHEN** body 无 `has-bg` 类
- **THEN** `--surface` 和 `--surface2` alpha 为 `1`

#### Scenario: 有背景图时 surface 半透明
- **WHEN** body 有 `has-bg` 类
- **THEN** `--surface` 和 `--surface2` alpha 约为 `0.38`（还原原 `has-bg` 规则中 `rgba(base,0.3)` 的混色结果）

### Requirement: CSS 静态 fallback
CSS `:root` SHALL 为四个派生变量提供不使用 `color-mix()` 的静态 fallback 值。

#### Scenario: JS 未执行时页面有基础颜色
- **WHEN** 页面 HTML 加载完成但 JS 尚未执行
- **THEN** 模块背景和边框显示为静态 fallback 颜色，不透明或不可见
