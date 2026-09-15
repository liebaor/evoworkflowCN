---
name: evo-bug
description: 通过紧凑 Failing Feedback Loop、Root-cause Analysis、最小修复和 Regression Coverage 诊断并修复已观察 Bug。适用于 Broken、Throwing、Failing、Flaky 或异常慢行为。
---

# EVO Bug

## 先读取
`.evo/project.md`、`.evo/context.md`、相关 Spec/Decision、Source/Tests 和 Environment Details。

## 循环
1. 明确 Observed vs Expected Behavior 和 Environment。
2. 通过最窄的真实 Entry Path 复现。
3. 建立一个会在该 Bug 上变红的紧凑反馈回路。可复现时，不要在没有有用信号前大范围理论推演。
4. 有价值时进一步最小化 Reproduction。
5. 基于 Code/Runtime Evidence 建立多个竞争 Hypothesis；需要时先 Instrument，再猜测。
6. 找到 Root Cause，以及 Repository 中本应成立的 Pattern/Invariant。
7. 做最小一致修复。
8. 增加/加强 Regression Coverage；若能由失败行为驱动，使用 `evo-tdd`。
9. 重跑 Focused Checks，并执行一个相关的组装后 Consumer Path。

Production/External Boundary 不可用时，该边界标记 UNVERIFIED，不能用 Source Inspection 冒充 Runtime Proof。

如果 Bug 改变 Accepted Intent → `evo-change`；如果暴露长期可复盘规则 → 更新 `.evo/decisions/`。

## 输出
报告 Reproduction、Root Cause、Fix、Regression Evidence 和剩余 UNVERIFIED Boundary。
