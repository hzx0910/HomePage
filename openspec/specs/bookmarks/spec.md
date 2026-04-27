## ADDED Requirements

### Requirement: 展示书签列表
系统 SHALL 按分组展示所有书签，每个书签显示 favicon 和标题。

#### Scenario: 正常展示
- **WHEN** 页面加载且配置中有书签数据
- **THEN** 系统按分组渲染书签，每个书签显示 favicon 图标和标题文字

#### Scenario: Favicon 加载失败降级
- **WHEN** favicon 图片加载失败（网络不可用、域名无 favicon 或所有候选 URL 均失败）
- **THEN** 书签图标位置显示主题色圆角矩形，中心为标题首字符（白色），不显示空白

#### Scenario: 无法生成 favicon URL 时显示字母头像
- **WHEN** 书签 URL 格式异常导致无法构造 favicon 请求 URL
- **THEN** 书签图标位置直接显示字母头像，不发起无效请求

#### Scenario: 字母头像随主题色变化
- **WHEN** 用户切换主题色后页面重新渲染
- **THEN** 字母头像背景色同步更新为新主题色

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

### Requirement: 编辑书签
用户 SHALL 能够编辑已有书签的分组、名称和链接。

#### Scenario: 触发编辑按钮
- **WHEN** 用户悬浮或长按某个书签
- **THEN** 书签左上角显示编辑按钮，右上角显示删除按钮

#### Scenario: 打开编辑表单
- **WHEN** 用户点击书签的编辑按钮
- **THEN** 弹出编辑表单，分组、名称、链接字段预填当前书签数据

#### Scenario: 保存编辑
- **WHEN** 用户修改字段后点击确认
- **THEN** 书签数据更新，列表重新渲染，变更保存到 localStorage

#### Scenario: 取消编辑
- **WHEN** 用户关闭编辑表单而不保存
- **THEN** 书签数据不变

### Requirement: 书签拖拽排序
用户 SHALL 能够通过拖拽调整书签在同一分组内的顺序，新顺序 SHALL 持久化到 localStorage。

#### Scenario: 同组内拖拽排序
- **WHEN** 用户将某书签拖拽到同一分组内另一书签的位置
- **THEN** 书签顺序更新，数据保存到 localStorage，页面重新渲染

### Requirement: 书签跨分组拖动
用户 SHALL 能够将书签从一个分组拖拽到另一个分组，书签 SHALL 归入目标分组并持久化。

#### Scenario: 跨分组拖动
- **WHEN** 用户将某书签拖拽到另一个分组的区域
- **THEN** 该书签的分组更新为目标分组，位置插入到目标位置，数据保存到 localStorage

### Requirement: 书签卡片布局
书签卡片 SHALL 隐藏标题行（`.card-header`），直接展示书签分组列表，无标题文字和独立添加按钮。待办卡片 SHALL 同样隐藏标题行。

#### Scenario: 书签卡片无标题行
- **WHEN** 页面正常加载
- **THEN** 书签卡片不显示「书签」标题和右侧 ＋ 按钮，内容区直接从书签分组开始

#### Scenario: 待办卡片无标题行
- **WHEN** 页面正常加载
- **THEN** 待办卡片不显示「待办」标题，内容区直接从添加待办按钮开始

### Requirement: 书签空态
书签列表为空时，系统 SHALL 显示一个可点击的「＋ 添加书签」按钮，点击后打开添加书签弹窗。

#### Scenario: 空态显示添加按钮
- **WHEN** 书签列表为空（无任何书签数据）
- **THEN** 书签区域显示「＋ 添加书签」按钮，不显示纯文字提示

#### Scenario: 点击空态按钮打开弹窗
- **WHEN** 用户点击空态「＋ 添加书签」按钮
- **THEN** 添加书签弹窗打开，行为与内联添加按钮一致

### Requirement: 弹窗背景透明度
添加书签弹窗和添加备忘弹窗 SHALL 使用半透明背景，与搜索推荐词区域视觉透明感一致，且背景色随主题色变化。

#### Scenario: 弹窗背景半透明
- **WHEN** 添加书签或添加备忘弹窗打开
- **THEN** 弹窗背景呈半透明效果，可隐约透出后方内容

#### Scenario: 弹窗背景随主题变化
- **WHEN** 用户切换主题色后打开弹窗
- **THEN** 弹窗背景色调随主题色同步更新
