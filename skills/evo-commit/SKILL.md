---
name: evo-commit
description: 为当前 bounded EVO 工作创建 AI-readable Git Commit，并在明确授权时可选 Push。适用于已验证工作、Goal Checkpoint，或用户要求 Commit/Push。Commit 记录状态，不证明正确性。
---

# EVO Commit

## 先读取
`git status`、相对目标 Base/Checkpoint 的 Diff、存在时的 `.evo/goal.md`、当前 Plan/Spec，以及真实存在的 Verification/Review Results。

## Preflight
1. 确认 Diff 属于一个一致 Goal/Slice；不要把无关用户工作一起提交。
2. 检查明显 Secrets、Credentials、Generated Junk、Accidental Large Files。
3. 区分 Verified Completion 与 WIP。缺 Evidence 不一定禁止用户明确要求的 Checkpoint Commit，但 Message 不能宣称完成。
4. 有 Repository Commit Convention 时遵守它。

## Message
优先使用面向 Outcome 的 Subject：

```text
<type>(<scope>): <outcome>
```

需要时使用便于人和未来 Agent 理解的 Body：

```text
Implements:
- S3 ...
- AC-4 ...

Verified:
- <实际执行的 command/path>

Context:
- .evo/specs/...
- .evo/plans/...
```

禁止伪造 `Verified` 条目。

## Commit
只 Stage 目标文件并 Commit；完成后重新读取 Status。

## Push
默认 **不 Push**。仅在以下情况 Push：
- 用户明确要求；或
- Active `.evo/goal.md` 明确授权 `push: true`。

普通 Feature Branch 使用 Non-force Push，必要时设置 Upstream。除非单独明确授权，绝不 Force Push、Push 到意外/默认受保护 Branch、Rewrite History 或 Bypass Hooks。

## 输出
返回 Commit SHA/Subject、Files/Scope、Message 中代表的 Verification、剩余 Working-tree Changes，以及执行过 Push 时的结果/Remote Branch。
