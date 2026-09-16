---
name: evo-recover
description: 在 Session 中断或切换 Agent/Harness 后，从 Repository Instructions、Tracker、Conformance Gates、Git 和 Evidence 重建真实当前状态，不依赖 Chat Memory 或 EVO State Database。
compatibility: "Codex、Claude Code、OpenCode；Tracker + Git aware"
disable-model-invocation: true
metadata:
  opencode/autoinvoke: "false"
---

# EVO Recover

## Purpose

在 Context Loss 或 Agent/Harness Switching 后恢复真实工程状态。

## Read order

1. Existing Standing Agent Instructions。
2. `docs/agents/repository.md`、Issue-tracker/Domain Configuration 和 Linked Authorities。
3. Active/Recent Parent Spec/Task，包括存在时的 `Repository Fit` / `evo-spec-review` State 和 Execution Envelope。
4. Open/Closed Ticket Graph、Dependencies、Per-ticket Repository Fit、Claims、Verification/Commit Comments。
5. 相关 `CONTEXT.md` / ADR。
6. Git Branch/Status/Diff/Recent Commits 和 Tracker References。
7. Current Source/Tests + Available CI/Runtime Results。

## Reconstruct

确定：

- Current Objective/Non-goals；
- Canonical Artifacts 和 Tracker Source；
- Spec Conformance Gate 是 Current/Missing/Blocked/Stale；
- Executable Ticket Frontier 在最近重大变化后是否已通过 `evo-plan-review`；
- 有 Commit/Evidence 支持的 Completed Work；
- Open Ready Frontier 和 Blocked Work；
- Uncommitted/Staged Changes 及其可能 Owning Ticket；
- Last Trustworthy Verification/Review Facts；
- Material Blockers/Unknowns；
- Repository Guidance、Representative Pattern、Reusable Capability Assumption 是否 stale/contradicted。

Tracker Status 本身不能证明 Behavior。没有相应 Evidence/Commit 的 Checked/Closed Item 要明确指出。同样，即使 Blocker 都 Closed，如果 Repository Fit Gate 缺失/stale，Open Ticket 也不是 Execution-ready。

## Output

输出紧凑 Handoff：Objective；Canonical Sources；Conformance Gate State；Completed/Verified；Worktree State；Ready Frontier；Blockers/Unknowns；Execution Policy；Exactly One Next Matt/EVO Skill。

除非用户明确要求，不要开始 Implementation。
