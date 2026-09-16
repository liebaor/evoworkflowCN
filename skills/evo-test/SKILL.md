---
name: evo-test
description: 手工触发一次较广、Risk-based、Project-native 的测试验收；条件允许时包含关键 User Journey，并默认不为测试引入新 Framework。
compatibility: "Codex、Claude Code、OpenCode；project-native tests/runtime；可选 Browser/E2E capability"
disable-model-invocation: true
metadata:
  opencode/autoinvoke: "false"
---

# EVO Test

## Purpose

当用户希望获得比普通 Implementation Loop 更广的信心时，显式运行一次 On-demand Test Pass。本 Skill **manual only**，不属于默认 `evo-goal` 生命周期。

使用 Repository 已有 Test Stack 和 Runtime Path。除非用户明确要求，不要仅为了满足本 Skill 新安装/引入 Test Framework。

## Read first

读取 Owning Spec/Ticket 或用户指定 Scope、`docs/agents/repository.md`、相关 Acceptance Criteria、已有 Test Commands/Config、Representative Tests、Application Run Instructions 和 Implementation Diff。

## Test selection

选择能对 Changed Behavior 提供有意义信心的最小测试集合。按顺序考虑，但只运行与本次 Change 相关的层级：

1. **Static/project checks** — build、compile、typecheck、lint 或项目等价检查。
2. **Focused behavior tests** — 已有 unit/service/component tests，覆盖变化规则。
3. **Integration/API tests** — Persistence、Transaction、HTTP/API Contract、Service Composition 等实际发生变化的 Boundary。
4. **Critical user journey** — 对 User-visible Behavior，在项目已有 Browser/E2E 或 Interactive Application Capability 可用时，通过真实 Application 执行关键 End-to-End Flow。

User Journey 示例：login → navigate → create/edit/search/delete，或该 Feature 的核心流程。

## Risk add-ons

仅在 Change 使其相关时增加：

- permission/auth → authorized + unauthorized/negative paths；
- data migration/schema → migration/compatibility checks；
- duplicate submission/transactional workflow → idempotency/concurrency-sensitive checks；
- external integration → boundary 可用时做 contract/real integration；
- 明确 performance-sensitive → 仅在项目已有能力时运行 performance/load checks。

不要把每次 `evo-test` 变成完整 QA Program。

## User simulation

Browser/Application interaction 可用时，像真实用户一样操作，不只看源码：

- 从正常 User Entry Point 开始；
- 使用 realistic data；
- 完成 Critical Happy Path；
- 尝试少量与 Feature 相关的高价值 Failure/Edge Action；
- 通过 Product Supported Interface 观察 Visible Result 和重要 Side Effect。

项目已有 Automated E2E 时优先复用，因为它可重复。Agent 交互式 Browser Operation 可以作为当前 Acceptance Evidence，但不能替代 Durable Automated Regression Coverage。

需要的 Browser/Application/External Boundary 无法真实执行时报告 `UNVERIFIED`，不能从低层测试推断 PASS。

## Status

- `PASS` — Selected Evidence 已实际执行/观察并支持行为；
- `FAIL` — 已执行 Evidence 与 Expected Behavior 冲突；
- `UNVERIFIED` — 必要 Boundary/Environment 不可用或未运行。

## Boundary

Testing 与 Implementation 分开。运行本 Skill 时不要偷偷修改 Production Code。失败时报告 Failing Evidence，并根据情况推荐 `diagnosing-bugs` 或 `evo-implement`；只有用户明确要求 Test-and-fix Loop 才继续修复。

## Output

简洁报告：Test Scope；实际执行的 Commands/Paths；Critical User Journey（若有）；`Behavior | Evidence | Status`；Failures 和下一 Diagnostic Step；重要 `UNVERIFIED` Boundary。
