---
name: evo-finish
description: "将已经 Verify/Review 的交付结果收敛为 Repository Current Truth，只更新真正的 Owners：Current Docs、Domain Context、ADR 和 Tracker State。"
compatibility: "Codex、Claude Code、OpenCode；Repository/Tracker-aware"
disable-model-invocation: true
metadata:
  opencode/autoinvoke: "false"
---

# EVO Finish

## Preconditions

Required Parent Acceptance 已 `PASS`，或相关 `UNVERIFIED` 已被明确接受，并且没有 `evo-review` Blocking Findings。

## Read first

读取 Source Spec/Parent Task、Ticket Graph/Comments、Final Verification/Review、Current Docs/Contracts、`CONTEXT.md`/Configured Domain Docs、ADR Convention、Repository Guide 和 Git Diff/History。

## Workflow

1. 只有 Shipped Behavior 真正改变时才更新 Current Product/API/Architecture/Operator Docs。
2. Domain Context 只记录 Stable Domain Vocabulary/Facts，不写成 Feature Log。
3. 只有满足 Repository Durable-decision Threshold 才创建/Supersede ADR。
4. 按 Tracker Protocol Reconcile/Close Parent Spec/Task 和 Remaining Tickets。删除与 Shipped Reality 冲突的过期 Future-tense Claims；历史讨论留在 Tracker/Git，不复制到别处。
5. 只有 Commands、Module Boundaries、Authorities 或 Representative Patterns 实质变化时才刷新 `docs/agents/repository.md`。
6. 清理 Document/Task 后检查 References。

## Boundary

Finish 不制造缺失 Implementation Evidence，不执行 Code Review，也不 Commit、Push、Merge、Tag、Release 或 Deploy。

## Output

报告改变的 Current-truth Owners、保留/新增 Durable Decisions、Reconciled Tracker Artifacts、Repository Guide Change 和明确接受的 Limitations。Finish 产生 Deliverable Diff 时下一步 `evo-commit`。