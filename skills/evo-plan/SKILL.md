---
name: evo-plan
description: 把已接受的 EVO Spec 或已理解 Change 拆成 `.evo/plans/` 下的 bounded vertical slices，使 Fresh Agent 可以独立实现和验证。多 Slice 实现或使用 `evo-goal` 前使用。
---

# EVO Plan

## 先读取
`.evo/project.md`、`.evo/context.md`、Owning Spec、相关 Decisions/Research、代表性 Code/Tests。

## Slice 契约
每个 Slice 记录：Objective 与覆盖的 Acceptance；Source of Truth（Spec/Decision 链接）；In Scope / Out of Scope；Existing Pattern/Reference Implementation；可能涉及的区域/文件（不把猜测写成事实）；Blocking Edges；Implementation Seam；Direct Verification Commands/Runtime Checks；可能需要收敛的 Docs/Context/Decision Surface。

优先沿真实 Consumer Path 做 vertical tracer bullet，而不是先 Database、再 Backend、再 Frontend 的横向批次。

## Fresh-Agent Test
假设把这个 Slice 和 Repository 单独交给一个全新 Agent。它必须知道改什么、不改什么、遵循哪个 Pattern、如何证明完成。如果仍依赖 Chat-only Knowledge，这个 Slice 就没准备好。

## 输出
写入/更新 `.evo/plans/<change>.md`，展示依赖顺序，并推荐 `evo-goal` 连续执行或 `evo-implement` 单步执行。
