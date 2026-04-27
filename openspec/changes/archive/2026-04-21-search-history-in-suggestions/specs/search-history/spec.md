## MODIFIED Requirements

### Requirement: 存储搜索历史
系统 SHALL 在每次搜索执行时，将搜索关键词追加到 `config.searchHistory` 数组，并立即通过 `Storage.save(config)` 持久化到 localStorage。若关键词已存在于历史中，SHALL 先移除旧条目再将其置于数组首位（最新优先）。历史 SHALL 最多保留 10 条，超出时删除最旧的条目。空字符串 SHALL NOT 被记录。`searchHistory` SHALL NOT 出现在导出的配置 JSON 文件中。

#### Scenario: 首次搜索写入历史
- **WHEN** 用户执行搜索且关键词不在现有历史中
- **THEN** 关键词被插入 `config.searchHistory` 数组首位，持久化到 localStorage

#### Scenario: 重复搜索去重置顶
- **WHEN** 用户搜索的关键词已存在于历史中
- **THEN** 该关键词从原位置移除并重新插入数组首位，历史总条数不变

#### Scenario: 超过 10 条时截断
- **WHEN** 搜索后历史条数超过 10
- **THEN** 最旧的条目被删除，历史保持不超过 10 条

#### Scenario: 导出配置不含搜索历史
- **WHEN** 用户点击"导出配置"按钮
- **THEN** 下载的 JSON 文件中不包含 `searchHistory` 字段
