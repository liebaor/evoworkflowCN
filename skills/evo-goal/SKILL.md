---
name: evo-goal
description: 在一个 Repository 内连续执行已准备好的多 Slice Plan 直到完成：实现、适合时 TDD、测试、诊断失败、Verify、Review、Finish，并创建已授权的 Checkpoint Commit。用户希望 EVO 一次持续完成所有小任务时使用。
---

# EVO Goal

## 目的
在没有独立 Workflow Runtime 的情况下提供受控连续执行。

编排边界必须明确：**one repository, one active goal, one writer**。EVO Goal 不是 Fleet Scheduler，也不是 Multi-repository Runtime。

## 前置条件
- `.evo/` 已初始化；
- Owning Spec 和 `.evo/plans/<change>.md` 已存在，重大 Human Decision 已确定；
- 一个 Checkout 只有一个 Writer；
- 不存在另一个 ACTIVE Goal。

## 启动 / 恢复
创建或更新 `.evo/goal.md`：

```markdown
# Goal
Status: ACTIVE

## Objective
...

## Source
Spec: .evo/specs/...
Plan: .evo/plans/...

## Execution policy
- tdd: when-appropriate
- checkpoint-commit: after-verified-slice
- push: false

## Progress
- [ ] S1 ...
- [ ] S2 ...

## Current
S1

## Last verified
...
```

从 Repository Evidence 恢复，不依赖 Chat Memory。

## 执行循环
对下一个未完成 Slice：
1. 重新读取 Slice、Governing Spec/Decisions 和相关 Source。
2. 应用 `evo-implement`；存在稳定 Behavior Seam 时应用 `evo-tdd`。
3. 工作中持续运行 Focused Project Feedback。
4. 使用 `evo-verify` 验证 Slice Acceptance。
5. 普通 FAIL：自行诊断/修复；Root Cause 不简单时使用 `evo-bug`；然后重新 Verify。不能因为普通代码/测试失败就停止。
6. 高风险或结构性重要 Slice 做 Focused `evo-review`；其他 Slice 可把完整独立 Review 延后到最终阶段。
7. 更新 `.evo/goal.md` 的 Progress/Current/Last verified。
8. Execution Policy 允许时，用 `evo-commit` 做 Commit-only Checkpoint。
9. 继续下一个 Ready Slice。

## 必须停下来找人的情况
需要未授权产品方向、付费/外部服务、重大隐私/安全暴露、破坏性/不可逆数据变更、Compatibility Break、重大架构边界、受保护凭据/生产授权，或 Spec 自身矛盾且 Repository Evidence 无法解决时，必须停止。

反复失败且已没有新的 Diagnostic Hypothesis/Evidence Path 时也停止，汇总尝试而不是死循环。

## 最终循环
全部 Slices 完成后：
1. 对整个 Spec Acceptance 和真实 Consumer Path 做 Full `evo-verify`。
2. 尽可能做独立 `evo-review`。
3. 解决 Findings，并按需重跑 Evidence。
4. `evo-finish` 收敛 Current Truth，并把 Goal 标为 COMPLETE。
5. `evo-commit` 做最终交付 Commit。
6. 只有 `.evo/goal.md` 明确 `push: true` 或用户明确要求时才 Push。

## 输出
完成时报告 Objective、完成 Slices、Final Evidence、Review Outcome、创建的 Commits、Push Status 和 Accepted Limitations。
