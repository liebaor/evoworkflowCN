---
name: evo-change
description: 将已接受需求的变化传播到真实 Spec/Tickets/ADR/Docs/Tests，同时保留未受影响的实现与证据，并只使真正受影响的 Repository Conformance Gate 失效。
compatibility: "Codex、Claude Code、OpenCode；Tracker-aware"
disable-model-invocation: true
metadata:
  opencode/autoinvoke: "false"
---

# EVO Change

## Purpose

显式治理 Requirement Evolution，不重写无关工作，也不创建第二 Source of Truth。

## Read first

读取 Canonical Old Spec/Parent Task、当前 Ticket Graph/Comments、Repository Fit、`docs/agents/repository.md`、相关 Domain/ADR、当前 Implementation/Tests/Docs、Git history/status 和已有 Verification Notes。

## Classify

将变化分类为一种或多种：

- clarification — wording 变化但 Accepted Outcome 不变；
- living revision — 未完成 Behavior/Scope/Acceptance 改变；
- evidence-driven refinement — 新事实解决旧 Unknown；
- stable reversal — 已交付 Durable Decision 被反转；
- independent decision — 出现新的重大 Trade-off。

## Delta

对 Outcome、Non-goals、Acceptance、Repository/Framework Fit、Tickets/Blockers、Code/Contracts、Tests/Evidence、Docs、Data/Migration/Compatibility、Decision Rationale 标记：

`RETAIN | REVISE | REMOVE | ADD`

## Apply to canonical owners

- 修改现有未完成 Spec/Parent Task，不创建 `final-v2` 副本。
- 保留未受影响的 Closed Tickets；只更新/重开 Delivered Acceptance 被失效的 Tickets；按需 Add/Remove Work 并记录原因。
- 通过配置的 Tracker Protocol 更新 Blocking Edges/Frontier。
- 只有 Domain Language/Facts 改变时才更新 `CONTEXT.md`。
- Durable Reversal 按 Repository ADR Convention 创建/Supersede ADR，不重写历史。
- 保留仍有效的 Implementation/Evidence；只有受影响 Acceptance 需要重新证明。
- 保留仍有效的 Repository Fit；只失效 Delta 触及的 Spec/Ticket Conformance Assumption。
- 不创建 `.evo/delta`、`.evo/state` 或 Duplicate Progress Ledger。

## Conformance invalidation

应用 Delta 后判断哪些 Gate 变 stale：

- 变化影响 Architecture Direction、Module Responsibility、Framework Capability Choice、Compatibility/Migration、Test Seam 或新增/移除重大 Abstraction → 重跑 `evo-spec-review`。
- Ticket 的 Module Fit、Representative Pattern、Reuse Capability、`REUSE/EXTEND/NEW`、Verification Pattern 或 Blocking Graph 变化 → 重跑相关 `evo-plan-review`。
- 未受影响 Gate 不为形式主义重复执行。

用户的新指令如果足够明确，已经授权 Changed Intent，就不要再要求仪式化二次确认。只有重大 Choice 仍模糊或跨越新的 Product/Security/Privacy/Data/Compatibility/Architecture Boundary 才停止。

## Output

给出简洁 Delta Table、变更的 Canonical Artifacts/Tickets、失效/保留的 Conformance Gates、失效/保留的 Evidence，以及新的 Ready Frontier 或 Next Skill。
