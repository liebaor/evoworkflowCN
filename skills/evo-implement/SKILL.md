---
name: evo-implement
description: 按 Repository Existing Pattern 实现一个 bounded plan slice，并持续使用真实反馈回路。Slice 的 Objective、Boundary、Acceptance 清楚时使用；Intent 改变时必须升级处理，不能偷偷改计划。
---

# EVO Implement

## 前置条件
读取 `.evo/project.md`、`.evo/context.md`、当前 Plan Slice、Owning Spec、相关 Decisions、Source/Tests，并在存在时至少找到一个代表性实现。重大 Human Decision 未解决时不要开始。

## 流程
1. 跟踪该 Slice 必须到达的真实 Consumer/Composition Path。
2. 复用已有 Permission、Response、Transaction、Data、Error、Logging、Component 和 Testing Pattern。
3. 行为存在稳定测试 Seam 时，使用 `evo-tdd`，不要先写大块实现。
4. 变更保持在 Slice 范围；无关发现单独记录。
5. 实现过程中持续运行 focused typecheck/tests/build/runtime checks。
6. 只有对应 Owner Fact 改变时才更新 Tests/Contracts/Current Docs。

## 升级处理
- Accepted Intent 变化 → `evo-change`；
- 缺少 Human 产品/架构 Decision → `evo-grill-with-docs`；
- 需要最新外部事实 → `evo-research`；
- 出现意外 Failure/Root-cause 问题 → `evo-bug`；
- Slice 比计划大很多 → 返回 `evo-plan`。

## 输出
报告准确变更、实际运行过的检查、跳过的检查和剩余不确定性。不要宣称整个 Goal 完成；Acceptance Proof 交给 `evo-verify`。
