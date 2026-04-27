## MODIFIED Requirements

### Requirement: 设置入口按钮
页脚工具栏 SHALL 在「导入」按钮右侧显示「设置」按钮，点击后打开设置弹窗（原内联面板替换为弹窗）。

#### Scenario: 点击设置按钮打开弹窗
- **WHEN** 用户点击「设置」按钮
- **THEN** 设置弹窗打开，其中包含背景图配置区域

### Requirement: 选择本地图片作为背景
系统 SHALL 允许用户通过设置弹窗内的文件选择器选择本地图片，将其设置为全页背景，并持久化存储。

#### Scenario: 选择图片后立即生效
- **WHEN** 用户在设置弹窗内点击「选择背景图」并选择一张本地图片文件
- **THEN** 系统将图片压缩至屏幕尺寸后转为 Base64 写入 `homepage_config.settings.backgroundImage`，页面背景立即切换为该图片

#### Scenario: 刷新后背景持久保留
- **WHEN** 用户设置背景图后刷新页面
- **THEN** 页面加载时从 localStorage 读取 Base64 并自动应用背景图

### Requirement: 移除背景图
系统 SHALL 允许用户在设置弹窗内移除当前背景图，恢复默认深色背景。

#### Scenario: 点击移除背景
- **WHEN** 用户在设置弹窗内点击「移除背景」且当前存在背景图
- **THEN** 系统将 `homepage_config.settings.backgroundImage` 置为 null 并保存，页面背景恢复为默认深色

#### Scenario: 无背景时移除按钮不可用
- **WHEN** 当前未设置背景图
- **THEN** 「移除背景」按钮显示为禁用状态（不可点击）

### Requirement: 背景图渲染与遮罩
系统 SHALL 将背景图以 `cover` 模式铺满整个 `body`，并在背景图上叠加半透明深色遮罩，保证页面内容在任意背景下可读。

#### Scenario: 背景图 cover 铺满
- **WHEN** 背景图已设置
- **THEN** 图片以 `background-size: cover; background-position: center` 铺满整个视口，不留白边

#### Scenario: 遮罩保证可读性
- **WHEN** 背景图已设置
- **THEN** 背景图上方叠加约 55% 不透明度的深色遮罩，页面所有卡片和文字颜色不变且清晰可读
