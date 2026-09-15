---
name: evo-verify
description: 使用项目原生 Tests、Build、Runtime Path 和直接观察验证 Accepted Outcome。Implementation/Bug Repair 后使用；每条 Acceptance 报告 PASS、FAIL 或 UNVERIFIED，不在 Verify 中偷偷修代码。
---

# EVO Verify

## 先读取
`.evo/project.md`、Owning Spec/Plan Acceptance、相关 Decisions、Implementation Diff，以及可用 Project Commands/Environments。

## Evidence Map
对每条 Acceptance 确认：1）Observable Behavior/Absence；2）Failure Surface；3）能推翻它的 Direct Evidence；4）准确 Command/Inspection/Runtime Path。

证据与风险匹配：Local Logic → Focused Unit Tests；Composition → Integration Tests；Persistence/Recovery → Replay/Resume；User-visible Behavior → Real App/Browser/API Path；External Service → 可用时真实 E2E；Deletion → Negative Search + Registration/Export/Docs/Tests 检查。

## 状态
- **PASS**：Direct Evidence 已实际执行/观察并支持该 Claim。
- **FAIL**：Direct Evidence 与 Claim 冲突。
- **UNVERIFIED**：需要的 Evidence 无法获得。

Static Inspection 只证明 Source Shape，不证明 Runtime Behavior；Build/Lint Green 只证明被编码的规则。

## 输出
使用表格：Acceptance | Evidence | Status | Scope/Notes。列出真正执行过的命令和跳过的 Boundary。

## 边界
Verify 不修 Implementation。FAIL → Implement/Bug；Intent 变化 → Change；通过验证后 → `evo-review`。
