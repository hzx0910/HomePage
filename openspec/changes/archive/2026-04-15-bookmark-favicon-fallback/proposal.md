## Why

书签图标通过 Google Favicons API 加载，当网络不可用或域名无 favicon 时，图片加载失败，当前降级处理是直接隐藏 `<img>`，书签左侧图标区域留空，视觉上不够完整。使用主题色 + 标题首字符作为默认图标，既保留图标位置的视觉一致性，又能快速辨识书签内容。

## What Changes

- favicon 加载失败（`onerror`）或无法生成 URL 时，用一个内联 SVG 占位图标替代，该图标：
  - 背景为主题色（`--accent`）的圆角矩形
  - 中心展示书签标题的第一个字符（白色）
- 图标尺寸与原 `<img>` 保持一致（14×14px）

## Capabilities

### New Capabilities

（无新能力，为现有书签展示功能的降级视觉增强）

### Modified Capabilities

- `bookmarks`: 书签 favicon 降级行为变更——从隐藏图标改为显示主题色字母头像

## Impact

- `index.html`：修改 `Bookmarks.render()` 中 favicon 失败的降级逻辑，新增生成 SVG 占位图的辅助函数
- 不改变 favicon 加载流程，仅处理失败态
