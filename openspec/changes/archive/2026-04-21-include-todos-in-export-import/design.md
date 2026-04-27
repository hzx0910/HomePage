## Context

现有 `config-storage` spec 在导出/导入场景中未明确提及 `todos` 字段。`index.html` 的实现已正确将整个 `cfg` 对象（含 `todos`）序列化导出，导入时也已校验 `Array.isArray(parsed.todos)`。本次变更仅补全规范文档，使规范与实现保持一致，不需要修改任何运行时代码。

## Goals / Non-Goals

**Goals:**
- 在 `config-storage` spec 中明确导出/导入必须包含 `todos` 字段的要求和校验场景

**Non-Goals:**
- 修改 `index.html` 的任何逻辑（实现已正确）
- 变更 todos 的数据结构
- 引入新的导出/导入 UI 交互

## Decisions

**仅修改 spec，不改代码**：经检查，`export()` 直接序列化完整 `cfg` 对象，`import()` 已校验 `Array.isArray(parsed.todos)`，实现无缺陷。最小变更原则下，只需更新 spec 补充缺失的文档要求。

## Risks / Trade-offs

- [低风险] spec 补充后若未来有人修改导出逻辑，需确保仍覆盖 todos → 已通过 spec 场景约束
