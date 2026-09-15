---
name: evo-change
description: 当工作已经开始后，Accepted Intent 发生变化时，更新 Canonical Working Spec/Plan/Decisions，并尽量保留不受影响的实现和 Evidence。
---

# EVO Change

## 先读取
`.evo/project.md`、`.evo/context.md`、Active Spec/Plan/Goal、相关 Decisions、当前 Implementation/Tests。

## 分类
- Clarification：文字澄清，Accepted Outcome 不变。
- Living revision：尚未完成的 Scope/Behavior/Acceptance 改变。
- Evidence-driven refinement：新观察事实解决 Unknown。
- Stable reversal：已经交付的长期 Decision 被反转。
- Independent decision：新的可复盘问题，有独立 Trade-off。

## Delta
对 Outcome、Non-goals、Acceptance、Rationale、Code/Contracts、Tests/Evidence、Current Docs、Migration/Compatibility 和 Decision Ownership，逐项标记 **retain / revise / remove / add**。

## 写入
- 未完成 Intent → 修改同一个 `.evo/specs/<change>.md`；
- Plan 受影响 → 修改 `.evo/plans/<change>.md`；
- Stable reversal → 新建并互相链接 `.evo/decisions/`，不要重写历史；
- Active Goal → 同步 `.evo/goal.md` Progress/Current Slice。

保留不受影响的 Implementation/Evidence，只重跑被 Delta 失效的证据。

## Human Stop
引入新产品方向、付费/外部服务、隐私/安全暴露、兼容性损失、破坏性数据变更或重大架构边界前必须询问人。

## 输出
提供简洁 Delta 表，并说明哪些 Artifacts/Evidence 仍然有效。
