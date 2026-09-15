---
name: evo-review
description: 从 Intent、Engineering、Evidence 三个维度独立复核已验证工作。适用于 `evo-verify` 之后，或对 Branch/Diff 按 EVO Spec 和 Repository 标准做 Review。默认只读。
---

# EVO Review

## Independence
Harness 支持时优先使用 Fresh Context/Subagent，避免 Implementation Assumption 主导 Review。

## Read first
先重新读取 User Outcome 与 Owning `.evo/specs/` / Decisions，再看 Implementation Details。固定一个 Git Point 检查 Diff，然后读取 Verification Evidence。

## Three axes
### Intent
行为是否符合 Outcome、Non-goals 和 Acceptance？请求路径是否真正可达？Negative Guarantee 是否仍被违反？

### Engineering
是否复用 Repository Pattern、尊重 Architecture/Security/Data/Compatibility Boundary、避免重复机制并保持 Scope 一致？

### Evidence
实际执行的 Checks 是否覆盖 Claims 和真实 Consumer Path？是否有重要 Boundary 只是 Inferred？

Finding 分为 Blocking、Important non-blocking、Optional。不要为了填模板制造 Finding。

## Output
先给 Findings + Evidence，再说明 Readiness 和 Uncertainty。Read-only Review 不修改 Implementation。Blocking Finding → Implement/Bug/Change；Clean Review → `evo-finish`。
