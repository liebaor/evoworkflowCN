---
name: evo-commit
description: 将已经理解清楚的 coherent engineering checkpoint 记录到 Git，并只执行明确授权的 Push；Commit 只描述状态，永远不创造正确性。
compatibility: "Codex、Claude Code、OpenCode；需要 Git"
disable-model-invocation: true
metadata:
  opencode/autoinvoke: "false"
---

# EVO Commit

## Core rule

**Commit describes state. It does not create state.**

Commit 记录已经存在的 Implementation/Evidence/Review Facts。它不能把 FAIL/UNVERIFIED/WIP 变成 Completed Work。

## Read first

读取 Git status/diff、Owning Spec/Ticket、实际 Verification/Review Results、Repository Commit Convention，以及 Active Goal Execution Envelope。

## Preflight

- Checkpoint 限定在一个容易理解的 Ticket/Stage/Fix/Final Convergence。
- 能安全分离时排除无关 User Changes；Scope 无法分离时停止。
- 检查明显 Credential/Secret、Generated Junk、Accidental Large Files。
- 区分 Verified Completion 与 Deliberate WIP/Error Checkpoint。
- Repository 有既有 Commit Convention 时遵守它。

## Message

优先使用简洁 Outcome-oriented Subject：

```text
<type>(<scope>): <outcome>
```

确有价值时再加入：

```text
Context:
- <owning ticket/spec>

Completed:
- <observable outcome>

Verified:
- <actual executed command/path/status>

Limitations:
- <meaningful limitation>

Next:
- <next tracker work or human action>
```

绝不能伪造 `Verified`。

## Commit authorization

用户明确要求 Commit，或处于已批准的 `evo-goal` Commit Policy 内，即授权 Scope 内普通 Commit。否则只准备 Message/Scope，并在真正创建 Commit 前请求授权。

## Push policy

默认 **no push**。

只有以下情况 Push：

- 用户明确要求；或
- Active Goal Execution Envelope 已授权该 Feature Branch/Remote 的 `final-only` / `per-ticket`。

正常 Push 必须 non-force。Force Push、History Rewrite、Unexpected/Default/Protected Branch、Merge、Tag、Release、Deploy 即使 Goal 允许普通 Push，也需要单独明确授权。

## Output

报告 Commit SHA/Subject、Included Scope、Represented Verification/Limitations、Remaining Worktree Changes，以及发生 Push 时的 Remote/Branch/Result。
