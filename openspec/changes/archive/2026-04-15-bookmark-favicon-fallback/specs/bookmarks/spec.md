## MODIFIED Requirements

### Requirement: Favicon 加载失败降级
书签 favicon 加载失败或无法获取时，系统 SHALL 显示一个以主题色为背景、书签标题首字符为内容的圆角矩形占位图标，尺寸与正常 favicon 一致。

#### Scenario: Favicon 加载失败显示字母头像
- **WHEN** favicon 图片加载失败（网络不可用或域名无 favicon）
- **THEN** 书签图标位置显示主题色圆角矩形，中心为标题首字符（白色），不显示空白

#### Scenario: 无法生成 favicon URL 时显示字母头像
- **WHEN** 书签 URL 格式异常导致无法构造 favicon 请求 URL
- **THEN** 书签图标位置直接显示字母头像，不发起无效请求

#### Scenario: 字母头像随主题色变化
- **WHEN** 用户切换主题色后页面重新渲染
- **THEN** 字母头像背景色同步更新为新主题色
