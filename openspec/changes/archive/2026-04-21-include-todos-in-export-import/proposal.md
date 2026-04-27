## Why

导出/导入配置的规范（`config-storage` spec）未明确说明待办项（todos）应包含在导出/导入数据中，导致规范与实现之间存在文档缺口，也无法保证未来修改时不意外遗漏 todos 数据。

## What Changes

- 在 `config-storage` spec 中明确：导出的 JSON 文件 SHALL 包含 `todos` 数组
- 在 `config-storage` spec 中明确：导入时 SHALL 校验 `todos` 字段存在且为数组，并完整恢复待办数据
- 在 `config-storage` spec 中明确：导入成功后页面重新渲染 SHALL 包含已恢复的待办列表

## Capabilities

### New Capabilities

（无新 capability，仅修订现有规范）

### Modified Capabilities

- `config-storage`: 补充导出/导入需包含 `todos` 字段的明确要求及校验场景

## Impact

- 仅修改 `openspec/specs/config-storage/spec.md`，无需改动 `index.html`（实现已正确）
- 无 API 变更，无破坏性变更
