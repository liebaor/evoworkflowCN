---
name: evo-init
description: 通过语义化 Repository archaeology 理解已有项目的权威规范、架构、命令、可复用能力和代表实现，让后续 EVO 开发沿用现有体系而不是创建平行结构。
compatibility: "Codex、Claude Code、OpenCode；Git Repository；与 Matt setup 集成"
disable-model-invocation: true
metadata:
  opencode/autoinvoke: "false"
---

# EVO Init

## Purpose

让 Fresh Agent 真正看懂这个 Repository，并建立未来代码应该如何融入现有系统的工程地图。这是 semantic repository archaeology，不只是 Framework detection。

## Preconditions

Matt setup 应已经定义 Issue Tracker 和 Domain Docs 约定。如果 `docs/agents/issue-tracker.md` / domain configuration 缺失，并且 `setup-matt-pocock-skills` 不可用，返回 `MATT_SKILL_REQUIRED: setup-matt-pocock-skills`。

## Read first

调查长期指令（存在时的 `AGENTS.md`、`CLAUDE.md`）、README/current docs、architecture/coding/contributing standards、manifest/lock、CI、formatter/linter/type/test 配置、application entry、representative source、tests、migrations/contracts、代码库中真实使用的 Framework/Platform convention，以及近期 Git history。

## Archaeology layers

1. **Explicit authorities** — 找出 Architecture、Coding Rules、Domain Language、API/Data Rules、Operations 的真正权威来源。
2. **Architecture** — 跟踪真实 Module Boundaries、Dependency Direction，以及至少一条代表性的 End-to-End Consumer Path。
3. **Operating paths** — 从 Repository Evidence 确认 build、test、typecheck/lint、run 和相关 observation commands。
4. **Existing patterns** — 找未来最可能涉及的 Representative Implementation：API/Controller、Service/Domain、Persistence、Permission/Auth、Transaction/Error、Frontend state/form/table、Migration、Tests 等。
5. **Reusable capabilities** — 识别已有 Framework-native class、helper、utility、shared module、component、annotation、middleware、data/access abstraction 和 extension point，后续应优先 reuse/extend。
6. **Conflicts/unknowns** — 暴露 docs 与 dominant code 的重要冲突、多套不兼容 Pattern 或缺失 Evidence。

优先选择广泛使用、当前仍有效且有测试的 Pattern，而不是孤立样例。明确的 Repository Rule 优先于通用偏好；如果文档规范和 dominant implementation 明显冲突，记录冲突，不要假装其中之一天然 canonical。

## Write

创建或刷新 `docs/agents/repository.md`，保持紧凑，至少包含：

- Authorities
- Build / Test / Run
- Architecture / Module Boundaries
- Representative Consumer Paths
- Existing Patterns (`Concern | Reference | Why this is representative`)
- Reusable Capabilities (`Concern | Existing capability | Typical use | Reference`)
- Development Contract
- Known Inconsistencies / Unknowns
- Observation commit/date

Reusable Capabilities 应覆盖最容易被 AI 重复发明的能力：标准 response、pagination、auth/permission、audit/logging、validation、persistence helper、transaction/error、cache、file/Excel/import-export、dictionary/status、frontend request/state/table/form、migration、test helper 等（仅在项目真实存在时记录）。

只链接 source/authority，不复制大段文档或源码。不要创建 `.evo/` 状态。

让项目现有 Agent instruction root 能指向 `docs/agents/repository.md`，同时保留用户原有指令。

## Development Contract

必须包含：

**Reference Before Edit** — 非机械实现修改前先找到最近的现有 reference，并将方案分类为 `REUSE`、`EXTEND` 或 `NEW`。

**Capability Before Creation** — 创建 shared class/helper/utility/component/middleware/base abstraction 或 Framework-like mechanism 前，先搜索 Repository / Framework capability map 的已有 owner。能 reuse/extend 就不要 new。

Framework-based Brownfield 项目里，当前 Repository 的真实 Framework 用法优先于通用教程；Framework-native capability 优先于平行 custom abstraction，除非已有接受的 Architecture Decision 明确允许。

## Stop

不要开始 Feature Implementation。若 Entry Point/Authority 冲突严重或关键文件不可访问，导致 Repository 无法安全解释，则停止。

## Output

总结已确认 Authorities、Representative Patterns、Reusable Framework/Project Capabilities、重要 Unknowns，以及 Repository 是否已具备 conformant planning/implementation 条件。
