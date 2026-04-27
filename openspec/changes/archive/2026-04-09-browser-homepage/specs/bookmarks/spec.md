## ADDED Requirements

### Requirement: 展示书签列表
系统 SHALL 按分组展示所有书签，每个书签显示 favicon 和标题。

#### Scenario: 正常展示
- **WHEN** 页面加载且配置中有书签数据
- **THEN** 系统按分组渲染书签，每个书签显示 favicon 图标和标题文字

#### Scenario: Favicon 加载失败降级
- **WHEN** favicon 图片加载失败（如离线状态）
- **THEN** 系统显示默认占位图标，不影响书签可点击性

### Requirement: 点击书签跳转
书签 SHALL 在新标签页打开对应 URL。

#### Scenario: 点击书签
- **WHEN** 用户点击任意书签
- **THEN** 系统在新标签页打开该书签的 URL

### Requirement: 添加书签
用户 SHALL 能够添加新书签，需填写标题、URL 和所属分组。

#### Scenario: 成功添加
- **WHEN** 用户填写标题和 URL 后确认添加
- **THEN** 新书签出现在对应分组中，数据保存到 localStorage

#### Scenario: URL 格式验证
- **WHEN** 用户输入不含协议的 URL（如 `github.com`）
- **THEN** 系统自动补全为 `https://github.com`

### Requirement: 删除书签
用户 SHALL 能够删除单个书签。

#### Scenario: 删除书签
- **WHEN** 用户对某书签触发删除操作并确认
- **THEN** 该书签从列表中移除，数据从 localStorage 更新

### Requirement: 书签分组
书签 SHALL 支持按自定义分组名称归类展示。

#### Scenario: 分组展示
- **WHEN** 书签数据包含多个不同分组
- **THEN** 系统以分组为单位分区块渲染书签

#### Scenario: 无分组书签
- **WHEN** 书签未指定分组（分组为空）
- **THEN** 系统将其归入默认分组"其他"
