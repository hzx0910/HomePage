## Why

不同用户对文字大小的偏好差异较大，固定字号无法满足所有使用场景（如高分辨率屏幕或视力需求）。通过在设置中提供字体大小选项，让用户一键调整全局文字大小。

## What Changes

- 在设置弹窗中新增「字体大小」配置区域，提供 5 档选择（1–5，默认 3）
- 用户选择后，页面所有文字大小随之同步调整
- 字体大小配置持久化存储到 `settings.fontSize`

## Capabilities

### New Capabilities

- `font-size`: 全局字体大小调节，5 档选择，持久化存储并实时应用

### Modified Capabilities

- `config-storage`: `settings` 对象新增 `fontSize`（number，1–5，默认 3）字段及旧配置兼容补填

## Impact

- `index.html`：设置弹窗 DOM、CSS 变量 `--font-scale`、Settings 模块逻辑、DEFAULT_CONFIG、Storage 迁移
