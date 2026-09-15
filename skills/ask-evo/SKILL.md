---
name: ask-evo
description: 读取当前 Repository，路由到唯一最合适的下一个 EVO Skill。适用于用户询问“下一步做什么”“如何继续”“现在做到哪了”或“不知道该用哪个 EVO 流程”的场景。只读。
---

# Ask EVO

## Purpose
基于 Repository 证据重建当前情况，并且只推荐一个下一步 Skill。

## Read first
1. 检查 `.evo/project.md` 和固定 `.evo/` 目录是否存在。
2. 如果存在，读取 `.evo/project.md`、`.evo/context.md`、存在时的 `.evo/goal.md`、相关 Spec/Plan/Decisions、Git status/diff/history，以及当前 Tests/CI 证据。

## Routing
- `.evo/` 缺失或结构不完整 → `evo-setup`。
- 工作区存在，但项目结构/build/test/pattern 尚未理解 → `evo-init`。
- 用户需要资深工程/架构指导 → `evo-advisor`。
- 重大产品/架构决策不清楚 → `evo-grill-with-docs`。
- 需要最新外部技术事实 → `evo-research`。
- 已达成一致的非机械需求需要 Working Spec → `evo-spec`。
- 已有 Spec/Intent，但缺 fresh-Agent 可执行 Slice → `evo-plan`。
- 用户希望连续完成整个已准备 Plan → `evo-goal`。
- 一个 bounded slice 已准备好 → `evo-implement`。
- 用户明确要求 test-first，或该行为适合稳定测试 seam → `evo-tdd`。
- 已接受 Intent 发生变化 → `evo-change`。
- 已观察到失败，需要诊断根因 → `evo-bug`。
- Acceptance 需要直接证明 → `evo-verify`。
- 已验证工作需要独立 Intent/Engineering/Evidence 复核 → `evo-review`。
- 已验证/复核工作需要知识收敛 → `evo-finish`。
- 工作需要进入 Git 历史，或用户明确要求 Push → `evo-commit`。
- 已有工作但当前 Session 上下文丢失 → `evo-recover`。

小型机械修改如果不涉及长期行为、Contract、架构、格式、测试策略或 Decision，可直接实现并做聚焦检查。

## Output
报告当前目标、已确认事实、Active `.evo/` Owner、重大 Unknown、实际进度、Blocker，以及一个唯一下一 Skill 和理由。

## Final checks
本 Skill 不修改文件、不实现功能，也不在内部执行目标 Skill。
