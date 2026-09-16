---
name: evo-implement
description: 使用 Repository 现有结构、Framework-native Capability 和 Representative Pattern 实现一个 bounded ticket；执行 Reference Before Edit 与 Capability Before Creation，并在 Git Delivery 前停止。
compatibility: "Codex、Claude Code、OpenCode；可选 Matt tdd/diagnosing-bugs capability"
disable-model-invocation: true
metadata:
  opencode/autoinvoke: "false"
---

# EVO Implement

## Purpose

交付一个 bounded vertical behavior，不引入平行架构、重复 Framework Capability，也不把 Git Delivery 混入 Implementation。

## Read first

读取 Owning Spec/Ticket、Acceptance Criteria、Tracker-backed 时的 `Repository Fit`、`docs/agents/repository.md`、相关 Standards/ADR/Domain Context、Affected Source/Tests，以及最近的 Consumer Path。

如果 Repository Guide 缺失或与当前 Code 严重冲突，先回 `evo-init`。如果已有 Planned Ticket Graph，而当前 Ticket 在最近重大变化后没有通过 `evo-plan-review`，先跑 Gate，不要在实现阶段临时发明 Plan。

## Reference Before Edit

非机械修改前：

1. 为每个重要 Concern 找最近的 Representative Implementation；
2. 跟踪被修改 Layer 的真实 Consumer Path；
3. 分类 `REUSE`、`EXTEND` 或 `NEW`；
4. 执行时重新打开真实 Reference/Capability Source，不只依赖可能过期的 Ticket Summary；
5. `NEW` 必须解释现有 Capability/Pattern 为什么不能扩展。

重大新 Architecture Boundary、Permission Mechanism、Persistence Model 或 Cross-cutting Abstraction 属于 Design/Decision Escalation，不是 Implementation Convenience。

## Capability Before Creation

新增 shared class/helper/utility/component/middleware/base abstraction、response/page wrapper、auth/permission、persistence wrapper、logging/audit、import/export helper 等 reusable capability 前：

1. 查 `docs/agents/repository.md` 的 Reusable Capabilities；
2. 打开相关 Framework/Project 的真实 Capability Implementation；
3. 搜索附近 Source 的等价用法；
4. 优先 `REUSE` / `EXTEND` 现有 owner；
5. 只有现有 Project/Framework Capability 无法满足 Accepted Requirement 时才 `NEW`，并在编码前暴露重大后果。

Repository-specific Framework Usage 高于通用教程和模型偏好的 Stack Pattern。RuoYi 项目通常应复用已有 response、pagination、security、logging、dictionary、DataScope、CRUD convention，而不是平行 Generic Abstraction。

## Workflow

1. 重述 bounded observable outcome 和 out-of-scope boundary。
2. 优先复用 existing modules/framework capabilities/helpers/contracts。
3. 有稳定 Behavioral Seam 且上游 `tdd` 可用时应用 `tdd`；不要假设 Harness-specific invocation syntax。不可用时继续使用 project-native focused tests，并明确说明未应用 upstream TDD。
4. 实现最小 coherent vertical change，同时遵守 Module Boundary 和 Ticket Repository Fit。
5. 运行触及路径所需的 focused type/test/lint/build feedback。
6. Accepted Intent 变化则进入 `evo-change`。
7. Difficult observed failure 需要 Root Cause 时应用 `diagnosing-bugs`；不要用重复猜测 Edit 掩盖失败。

## Stop

遇到未解决 Product Meaning、Breaking Compatibility、重大 Architecture/Security/Privacy Choice、Destructive Data Action、意外 Paid/External Dependency、Protected Credential/Production Authorization、或改变 Acceptance 的 Scope Expansion 时停止。

## Output

报告 Outcome、`REUSE/EXTEND/NEW` References、实际 Reuse/Extend 的 Capability、任何 NEW 的理由、Changed Areas、实际运行的 Focused Checks、Remaining Uncertainty 和 Next Step（`evo-verify`）。不要 Commit/Push。
