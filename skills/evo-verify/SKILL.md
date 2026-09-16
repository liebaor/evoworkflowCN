---
name: evo-verify
description: 使用直接、项目原生的 Evidence 证明每条 Acceptance Claim，并诚实报告 PASS、FAIL 或 UNVERIFIED，不在验证阶段偷偷修改实现。
compatibility: "Codex、Claude Code、OpenCode；project-native tests/runtime/CI"
disable-model-invocation: true
metadata:
  opencode/autoinvoke: "false"
---

# EVO Verify

## Purpose

回答 Requested Behavior 是否真的有 Evidence 支持，而不是看实现“似乎合理”就判定完成。

## Read first

读取 Owning Spec/Ticket Acceptance Criteria、Repository Verification Commands、Implementation Diff 和当前可用 Environment/Runtime Path。

## Evidence map

每条 Acceptance Criterion 明确：

1. Observable Behavior 或必须不存在的行为；
2. Likely Failure Surface；
3. 能支持/反驳它的 Direct Evidence；
4. 实际要执行的 Test/Build/Runtime/Inspection Path。

Evidence 与 Risk 匹配：Local Logic 优先 Focused Test；Composition/Persistence 用 Integration；用户可见行为尽量走真实 API/Browser/Application Path；External E2E 只有 Boundary 真可用时才算 Direct Evidence。

## Status

- **PASS** — Direct Evidence 已实际执行/观察，并支持 Claim。
- **FAIL** — Direct Evidence 与 Claim 冲突。
- **UNVERIFIED** — 所需 Direct Evidence 不可用或未执行。

Static Source Inspection 只证明 Source Shape，不证明 Runtime Behavior。Build/Lint Green 只证明工具实际检查的规则。

## Persistence

在 Tracker-backed Goal 下或 Evidence 值得长期保留时，按 Tracker Protocol 在 Owning Ticket 写简洁 Verification Summary。不要创建独立 EVO Evidence Database。

## Boundary

Verify 内不要修代码。FAIL 返回 `evo-implement` 或上游 `diagnosing-bugs`；Accepted Intent 变化进入 `evo-change`。

## Output

返回 `Acceptance | Evidence | Status | Scope/Notes`，列出真正执行的 Commands/Paths，以及 skipped/unavailable boundaries。
