## ADDED Requirements

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
