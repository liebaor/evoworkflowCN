---
name: ask-evo
description: 只负责判断当前软件工程场景下一步最适合使用哪个 Matt 或 EVO Skill，并且只推荐一个，不直接执行工作。
compatibility: "Codex、Claude Code、OpenCode；建议同时安装 Matt engineering Skills"
disable-model-invocation: true
metadata:
  opencode/autoinvoke: "false"
---

# Ask EVO

## Purpose

作为 Matt engineering Skills + EVO extensions 之上的只读路由器。根据当前真实 Repository / Tracker 状态，只推荐一个最合适的下一 Skill/capability。

## Read first

读取项目长期 Agent 指令、存在时的 `docs/agents/issue-tracker.md`、`docs/agents/domain.md`、`docs/agents/repository.md`、相关 Tracker 状态（包括 Repository Fit）、Git status 和用户当前意图。不要为了路由而创建缺失的项目产物。

## Routing

- Matt setup/config 缺失 → `setup-matt-pocock-skills`。
- Repository 工程结构/Pattern/Capability 未理解，或 Guide 明显过期 → `evo-init`。
- 用户需要基于真实 Repository 的高级工程/架构建议 → `evo-advisor`。
- 产品/Domain 含义不清 → `grill-with-docs`；如果主要是 Domain language/modeling → `domain-modeling`。
- 需要当前外部事实 → `research`。
- 已稳定的意图需要形成 Spec → `to-spec`。
- Canonical Spec 已存在，但在最近一次重大变化后没有通过 Repository Fit → `evo-spec-review`。
- 已 Review 的 Spec 需要拆成 Agent-sized vertical tickets + blockers → `to-tickets`。
- Ticket Graph 已存在，但在最近一次重大 Spec/Architecture/Capability 变化后没有通过 Repository Fit → `evo-plan-review`。
- 工作过大/不确定，超出单 Session，需要先建立 Decision Map → `wayfinder`。
- 一个 bounded reviewed ticket 需要按 EVO delivery semantics 实现 → `evo-implement`。
- Accepted intent 已变化 → `evo-change`。
- 复杂 Bug / performance regression 需要系统诊断 → `diagnosing-bugs`。
- Acceptance claim 需要直接证据 → `evo-verify`。
- Worktree/branch 需要交付前 Conformance Review → `evo-review`。
- 用户明确要求进行一次更广的测试/用户模拟 → `evo-test`。
- 已通过 Conformance Review 的 Ticket Graph 需要持续执行 → `evo-goal`。
- 最终已 Verify/Review 的工作需要 Current Truth convergence → `evo-finish`。
- 一个 coherent checkpoint 需要 Commit 或已授权 Push → `evo-commit`。
- Fresh/interrupted Session 需要重建当前工作 → `evo-recover`。

如果最佳路线是当前 Session 无法加载的 Matt Skill，返回 `MATT_SKILL_REQUIRED: <id>`，不要用 EVO 模仿版替代。

## Output

返回 `Next: <skill-id>`，再用 1–3 句话说明基于当前 Repository/Tracker Evidence 的理由。不要执行下一 Skill。
