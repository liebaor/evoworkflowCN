---
name: evo-review
description: 在 EVO Delivery 前审查未提交或已提交工作，覆盖 Repository Conformance、Accepted Intent 与 Evidence，并能看到上游 commit-range review 可能看不到的 Worktree Change。
compatibility: "Codex、Claude Code、OpenCode；Git worktree 或 commit diff"
disable-model-invocation: true
metadata:
  opencode/autoinvoke: "false"
---

# EVO Review

## Purpose

提供独立的交付前 Review，同时支持未提交 Goal Output 和 Committed Diff。

如果 fixed-point committed-diff Workflow 更合适，直接使用上游 `code-review`。本 Skill 存在是因为 EVO Goal 通常在 `evo-commit` 前 Review，需要看到 Worktree/Staged Changes。

## Read first

读取 Owning Spec/Ticket、Repository Fit、`docs/agents/repository.md`、Standards/ADR、相关 Reference Implementations 和 Reusable Capability Owners、Verification Result、Git status，以及完整 Intended Diff。

## Axes

### Repository Conformance

检查是否遵守 Documented Rules、Module Boundaries、Existing Contracts 和声明的 `REUSE/EXTEND/NEW`。

重点检查：

- 没有充分理由却偏离 Representative Implementation；
- 已有 Project/Framework Capability 时又建立 Duplicate Helper/Utility/Component；
- 平行 response、pagination、auth/permission、persistence、logging/audit、validation、state 或 infrastructure mechanism；
- Responsibility 放错层或 Dependency Direction 违规；
- 遵循通用 Framework Advice 却忽视当前 Repository 的真实 Framework Usage；
- 绕过 Capability Before Creation 的 `NEW` Abstraction。

### Intent

Diff 是否完整满足 Accepted Outcome/Non-goals，且没有 Missing Behavior 或 Scope Creep？

### Evidence

现有 Verification 是否真的覆盖重要 Claim 和真实 Consumer Path？明确指出只是 Inference 的 Claim。

Finding 分类：`BLOCKING`、`IMPORTANT`、`OPTIONAL`。不要为了填模板硬造问题。

Duplicate/Parallel Cross-cutting Capability 通常是 `BLOCKING`，除非 Accepted Spec/ADR 明确授权新 Architecture。

## Independence

Harness 支持 Fresh Context/Subagent 时优先使用独立 Review Context，但不要绑定某一种 Subagent API。

## Output

Findings First；每条尽量关联 Evidence/Path/Acceptance。随后报告 Readiness、Repository Fit Conformance、Reused/New Capabilities 和 Remaining Uncertainty。Review 阶段不要修改 Implementation。
