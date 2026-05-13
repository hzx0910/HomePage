## MODIFIED Requirements

### Requirement: 背景图渲染与遮罩
系统 SHALL 将背景图以 `cover` 模式铺满整个 `body`，并在背景图上叠加半透明深色遮罩，保证页面内容在任意背景下可读。应用或移除背景图时，系统 SHALL 重新调用 `applyAccent()` 以同步更新 surface 颜色变量的透明度。

#### Scenario: 背景图 cover 铺满
- **WHEN** 背景图已设置
- **THEN** 图片以 `background-size: cover; background-position: center` 铺满整个视口，不留白边

#### Scenario: 遮罩保证可读性
- **WHEN** 背景图已设置
- **THEN** 背景图上方叠加约 55% 不透明度的深色遮罩，页面文字清晰可读

#### Scenario: 应用背景图后 surface 变为半透明
- **WHEN** 用户设置背景图后
- **THEN** `--surface` 和 `--surface2` alpha 约为 `0.38`，卡片模块透出背景图

#### Scenario: 移除背景图后 surface 恢复不透明
- **WHEN** 用户移除背景图后
- **THEN** `--surface` 和 `--surface2` alpha 为 `1`，卡片模块为纯色背景
