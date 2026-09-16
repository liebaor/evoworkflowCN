---
name: evo-goal
description: 在 Repository Conformance Gates 之后，在批准的 Execution Envelope 内持续执行 prepared tracker-backed Ticket Graph：Implement、Verify、Review、Commit、Close、Advance，直到完成或真正的语义/风险边界停止。
compatibility: "Codex、Claude Code、OpenCode；Tracker Protocol + Git；可选 Matt tdd/diagnosing-bugs"
disable-model-invocation: true
metadata:
  opencode/autoinvoke: "false"
---

# EVO Goal

## Purpose

Delegate execution, not ambiguity。让 Ready Work 连续完成，不需要中央 State Runtime，也不为普通工程阶段反复请求 Human Approval。

## Preconditions

- Matt setup 已配置 Issue Tracker/Domain Layout。
- `evo-init` 已建立当前 Repository Guidance。
- Canonical Spec/Parent Task 存在，Acceptance 足够执行。
- 最近重大 Accepted-Intent Change 后 Spec 已通过 `evo-spec-review`。
- Canonical Ticket Graph 和 Blocking Edges 足够执行。
- 最近重大 Spec/Architecture/Capability Change 后 Ticket Graph 已通过 `evo-plan-review`，可执行 Tickets 有足够 Repository Fit。
- 启动所需 Product/Architecture/Security/Data Choice 已解决。
- One checkout has one active writer。

Conformance Gate 缺失/stale 时先回相应 Gate，不要在 Execution Loop 内自行发明 Repository Fit。

## Execution Envelope

开始前确定，并在 Cross-session Continuation 需要时持久化在 Canonical Parent Task/Local Tracker：

- Source Spec / Parent Task；
- Scope/Ticket Graph；
- Commit Policy：通常 `per-ticket`；
- Push Policy：`none`（默认）、`final-only`、`per-ticket`；
- Push 已授权时的 Target Branch/Remote；
- Human-stop conditions / special constraints。

Tracker owns progress。不要把 Ticket checkbox/status 镜像到 `.evo/goal.md` 或 `.evo/state.yml`。

## Loop

只要 Tracker Frontier 有 Ready Work：

1. 选择一个 Open、Unblocked、Conformance-reviewed Ticket；Tracker 支持 Claim/Assignee 时 Claim。
2. 记录当前 Git Base，界定 Delivery Diff。
3. 对 Ticket 应用 `evo-implement`；Reference Before Edit + Capability Before Creation 是执行不变量。
4. 应用 `evo-verify`。
5. 普通 FAIL（test/build/lint/code behavior）由 Agent 诊断并修复，不找人。非简单 Root Cause 可用 `diagnosing-bugs`，然后 Re-verify；只有重复失败已经没有新 Hypothesis/Evidence Path 才停止。
6. 对完整 Pre-commit Diff 应用 `evo-review`。解决 Blocking Finding，包括 Duplicate/Parallel Capability，再按需重新 Verify/Review。
7. 按 Envelope 的 Commit/Push Policy 应用 `evo-commit`。Goal Invocation 预授权 Scope 内普通 Commit；Push 只遵守显式 Envelope Policy。
8. 按 Tracker Protocol Update/Close Ticket，并写 Verification/Commit Facts。
9. 从 Tracker 重算 Frontier，不信任 Cached Progress。

Accepted Intent 变化导致 Ticket 无效时进入 `evo-change`，更新 Canonical Owners/Frontier，只重跑失效的 Conformance Gate，然后继续。

## Human stop

遇到未解决/新的 Product Direction、Breaking Compatibility、重大 Architecture Boundary、Security/Privacy Exposure、Destructive/Irreversible Data、New Paid/External Service、Missing Protected Credential/Production Authorization、Ambiguous Target Branch/Remote、Exhausted Diagnosis 时停止。

**不要**仅因 compile error、failing tests、lint/type error、ordinary bug、review finding 停止。

## Finalization

Scope 内无剩余 Tickets：

1. 针对 Parent Acceptance 和真实 Consumer Paths 运行 full `evo-verify`；
2. 针对完整 Goal Diff/History 运行 final `evo-review`；
3. 解决 Blocking Findings，并重新证明受影响 Acceptance；
4. 应用 `evo-finish`；
5. Finish 改变 Current-truth Artifact 时应用 final `evo-commit`；
6. 只有 Envelope 明确授权才 Push。

`evo-test` 不属于上述默认生命周期，只能用户手工触发。

## Output

报告 Completed Tickets、Conformance Gate Status、Verification/Review Status、Commits、Tracker State、Push Status 和已接受/未验证限制。
