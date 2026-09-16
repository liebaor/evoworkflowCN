---
name: evo-spec-review
description: 在 Ticket Planning 前审查 canonical Spec；若修正明确且不改变产品意图，则直接修正，使实现方向符合 Repository 现有架构、Framework Capability 和 Compatibility Constraints。
compatibility: "Codex、Claude Code、OpenCode；需要 evo-init Repository Guide + canonical Spec"
disable-model-invocation: true
metadata:
  opencode/autoinvoke: "false"
---

# EVO Spec Review

## Purpose

防止一个“技术上看似合理”的 Spec 把后续实现带离 Repository 已有架构或 Framework-native Capability。

这是轻量 Architecture/Repository-Fit Gate。它不替代上游 `to-spec`，不创建平行 Spec，也不能把 Product Spec 变成逐文件 Implementation Plan。

## Preconditions

- `evo-init` 已生成最新 `docs/agents/repository.md`。
- Canonical Spec/Parent Task 已存在，通常来自上游 `to-spec`。

缺任何一个前置条件时路由到相应 Skill，不要猜。

## Read first

读取完整 Canonical Spec、`docs/agents/repository.md`、Architecture/Coding Standards、相关 ADR/Domain Docs、Representative Implementations 和对本方案有实质影响的 Reusable Capabilities。

## Review axes

### Repository architecture fit

检查 Proposed Direction 是否遵守现有 Module Boundary、Dependency Direction、Contract、Data/Permission Convention 和 Extension Point。

### Framework-native fit

检查 Repository/Framework 是否已经提供 Spec 需要的机制：response/pagination abstraction、auth/permission、audit/logging、validation、persistence helper、dictionary/state infrastructure、frontend component、test seam、migration 等。

### Capability Before Creation

Spec 要认可新的 cross-cutting abstraction、shared helper、middleware、utility、component、service base、response/page/auth layer 或 Infrastructure Mechanism 前，先确认没有等价的 Repository/Framework Capability。

架构/Capability 层将方向分类为 `REUSE`、`EXTEND` 或 `NEW`。`NEW` 必须解释现有能力为什么无法满足。

### Compatibility and migration

显式暴露 Breaking API/Data/Permission/Behavior Change、Migration 和 Compatibility Risk，再进入 Ticketing。

### Testability

尽量使用现有 Behavioral Seams 和 Repository-native Test Path，不创建平行测试架构。

## Canonical update

不要创建 Review Sidecar Document。

如果 Repository Evidence 足够明确且 Product Intent 不变，直接更新 canonical Spec，增加/修正简洁的 `Repository Fit`（或等价）Implementation Constraints。优先记录稳定 Module/Capability/Symbol Reference，不写脆弱行号或大段 Code Snippet。

Repository Fit 应回答：

- 扩展哪个现有 Architecture/Module Boundary；
- 必须复用哪些 Framework/Shared Capabilities；
- 哪个 Representative Pattern 约束 Solution Shape；
- Direction 属于 `REUSE` / `EXTEND` / `NEW`；
- 是否存在合理的新 Abstraction 或 Compatibility Constraint。

如果解决冲突需要新的重大 Product/Architecture/Security/Data Decision，不要替用户决定。报告 `BLOCKED` 并路由到对应 Human/Design Decision Path。

## Status

- `READY` — Spec 已符合要求，或只做了非重大 wording normalization。
- `REVISED` — Canonical Spec 已按确认的 Repository Constraint 修正，且 Product Intent 未变。
- `BLOCKED` — 未解决的重大选择阻止安全 Ticket Planning。

## Output

报告 Status、支配实现的重要 Repository/Framework Capabilities、Canonical Spec Edits、未解决重大选择，以及 READY/REVISED 后的 Next Step（`to-tickets`）。
