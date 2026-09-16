---
name: evo-plan-review
description: 在执行前审查并规范化 canonical Ticket Graph，使每个 Slice 都符合 Repository 现有模块、Framework-native Capability、Reusable Utility/Component 和 Representative Pattern。
compatibility: "Codex、Claude Code、OpenCode；需要 evo-init Repository Guide + tracker-backed tickets"
disable-model-invocation: true
metadata:
  opencode/autoinvoke: "false"
---

# EVO Plan Review

## Purpose

在 Implementation 前把 Repository Conformance 变成显式 Gate。上游 `to-tickets` 负责 Vertical Slicing 与 Blocking Edges；本 Skill 检查这些 Tickets 是否按照“这个 Repository 实际应该如何扩展”的方式规划。

不要创建第二份 Plan/Review Ledger。如果修正是机械性的且不改变 Intent，直接修 canonical tickets。

## Preconditions

- `evo-init` 已产生最新 `docs/agents/repository.md`。
- Canonical Spec 在最近重大 Accepted-Intent Change 后已经通过 `evo-spec-review`。
- Canonical Ticket Graph 已存在，通常来自 `to-tickets`。

## Read first

读取完整 Spec/Parent Task、Scope 内全部 Ticket 与 Blocker、`docs/agents/repository.md`、相关 Standards/ADR/Domain Context、Source/Tests，以及支配规划工作的 Representative Implementations/Capabilities。

## Review every ticket

每个 Ticket 都建立简洁 Repository Fit Contract。

### Module fit

明确 Slice 扩展哪个现有 Module/Boundary，Dependency Direction 是否符合 Repository Architecture。

### Representative implementation

找出 Ticket 关键 Concern 最近的 Production Pattern。优先稳定 Symbol/Module/Guide Reference，不用脆弱行号或复制代码。

### Capability Before Creation

Ticket 要新建 shared utility/helper/base class/middleware/response-page abstraction/permission-auth/persistence wrapper/frontend component infrastructure 等 reusable mechanism 前，先搜索 Repository/Framework Capability Map 和真实 Source。

### Reuse strategy

分类：

- `REUSE` — 组合/使用已有 Capability，不修改其 abstraction；
- `EXTEND` — 在已有 Pattern/Extension Point 内增加行为；
- `NEW` — 真正引入新的 Capability/Abstraction。

`NEW` 必须解释现有 Framework/Repository 为什么不能满足需求。重大 Architecture/Security/Data/Compatibility 影响不会被本 Skill 自动批准。

### Verification fit

明确应使用哪个 Repository-native Test/Verification Pattern。优先现有 Seam 和真实 Consumer Path，不创建平行测试架构。

## Preserve good ticket design

不要为了 Repository Conformance 把 `to-tickets` 的 tracer-bullet vertical slice 改回按层 Horizontal Ticket。除非 Repository Evidence 证明 Graph 本身无效，否则保留 Vertical Behavior、Blocking Edges、Fresh-context Sizing。

## Canonical update

如果不改变 Accepted Product Intent 就能修正，直接编辑 canonical ticket。需要时增加 `Repository Fit`：

- Module / boundary
- Reference pattern
- Reuse capabilities
- Strategy: `REUSE | EXTEND | NEW`
- New abstraction justification（仅 NEW）
- Verification pattern

已有 Repository/Framework Capability 是明确 owner 时，移除计划中的 duplicate abstraction。

如果 Ticket Graph 提议重大不同 Architecture、Breaking Compatibility、Destructive Data Path、新 Security Model 或其他未解决 Decision，报告 `BLOCKED`，不要静默“规范化”掉。

## Gate status

- `READY` — 所有可执行 Ticket 具有足够 Repository Fit，无重大未解决问题。
- `REVISED` — Canonical Tickets 已修正/补充，现在 Ready。
- `BLOCKED` — 至少一个重大 Decision 阻止安全执行。

`evo-goal` must not begin on an unreviewed or BLOCKED ticket graph. `evo-change` 使 Architecture/Capability Assumption 失效时，恢复前重新运行受影响 Gate。

## Output

报告 Gate Status、修改的 Tickets、阻止的 Duplicate/New Capabilities、未解决 Decisions 和 Ready Frontier。不要实现代码。
