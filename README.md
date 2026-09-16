# EVOworkflow 2.0

> 面向长期 AI 软件工程的兼容优先扩展层，建立在 Matt Pocock 原始 Skills 之上，同时保持上游 Skill ID、结构和工程语义稳定。

`evoworkflowCN` 是 [`liebaor/evoworkflow`](https://github.com/liebaor/evoworkflow) 的中文镜像。英文仓库是 canonical source；本仓库保持相同的目录结构、Skill ID、文件名、命令、路径、代码标识和机器字段，并将面向人的正文翻译为中文。

**Markdown headings 保持英文。** `name`、metadata key、命令、文件路径、代码、协议字段和 API 名称保持英文。MIT License 等法律文本保留上游原文。

```text
Matt Skills                  EVO Extensions
───────────                  ──────────────
domain-modeling              evo-init
grill-with-docs              evo-spec-review
research                     evo-plan-review
to-spec                      evo-implement
to-tickets                   evo-change
wayfinder                    evo-verify
tdd                          evo-review
diagnosing-bugs              evo-test
codebase-design              evo-goal
code-review                  evo-finish
                             evo-commit
                             evo-recover
                             evo-advisor
                             ask-evo
```

## Core boundary

**Matt is upstream. EVO is an extension, not a fork.**

- 英文仓库 vendoring Matt 的正式 Engineering + Productivity Skills；中文仓库同步同一组 Skill，并翻译其人类可读内容。
- 中文化不会改变 Skill ID、目录结构、命令、代码标识或核心行为。
- EVO 需要不同生命周期时使用独立的 `evo-*` Skill，不覆盖 Matt 原始 Skill ID。
- Issue Tracker 继续拥有 Spec/Ticket 的进度和依赖；不会重新建立 `.evo/state.yml`。
- Source、tests、current docs、`CONTEXT.md`、ADR、Tracker、Git 和 CI 共同构成项目事实来源。

同步来源和翻译规则见 [`UPSTREAM.md`](UPSTREAM.md)。

## Installation

中文用户可以直接使用本仓库作为单一 Skill 来源：

```sh
npx skills@latest add liebaor/evoworkflowCN
```

不要在同一目标重复安装 `mattpocock/skills` 或英文 `liebaor/evoworkflow`，避免重复的 Matt Skill ID。

项目首次接入：

```text
setup-matt-pocock-skills
→ evo-init
→ ask-evo
```

`setup-matt-pocock-skills` 仍然负责 Matt 的 Issue Tracker / domain docs 配置；`evo-init` 负责理解当前 Repository 实际应该如何扩展。

## Development contract

### Repository understanding

`evo-init` 会调查显式规范、架构和模块边界、真实 consumer path、build/test/run 命令、代表实现、Framework/Utility/Component 可复用能力，以及文档与代码之间的冲突。

结果写入：

```text
docs/agents/repository.md
```

它是地图，不是复制整个代码库的百科全书。

### Reference Before Edit

非机械修改前必须找到最接近的现有实现，并将方案分类为：

```text
REUSE | EXTEND | NEW
```

`NEW` 必须解释为什么现有结构无法满足；重大新架构不能作为实现阶段的随手选择。

### Capability Before Creation

新增公共 Helper、Utility、Component、Base abstraction、Response/Page wrapper、Permission/Auth、Persistence wrapper、Middleware、Logging/Audit 等可复用能力之前，必须先搜索 Repository 和 Framework 是否已有 owner。

默认优先级：

```text
Human-approved intent
→ documented repository rules
→ representative production pattern
→ existing repository/framework capability
→ framework official convention
→ general engineering heuristic
→ new abstraction
```

在 RuoYi 等 Brownfield 项目里，应优先复用项目已有的响应、分页、权限、日志、字典、DataScope、CRUD 和前端约定。

### Planning Conforms Before Execution

Matt 的 `to-spec` / `to-tickets` 保持原始职责，EVO 在其后增加 Repository Conformance Gate：

```text
to-spec
→ evo-spec-review
→ to-tickets
→ evo-plan-review
```

`evo-spec-review` 检查方案层的架构/Framework Fit；`evo-plan-review` 检查每个 Ticket 的 Module Fit、Reference、Capability reuse、`REUSE/EXTEND/NEW` 和项目原生验证方式。

`evo-goal` 不应在 Spec/Plan Gate 缺失、失败或已经过期时启动。

### Human owns meaning; Agent owns execution

人负责产品意图、重大架构/安全/数据决策、风险接受和外部授权。进入已批准的 **Execution Envelope** 后，Agent 可以连续执行机械性的开发、验证、修复、Review、Commit 和下一 Ticket。

### Tracker owns progress

EVO 2.0 没有 `.evo/state.yml`、阶段数据库或第二份 Ticket 进度。Tracker 是 Spec/Ticket/Blocking/Progress 的唯一 owner；Git 保存历史；tests/runtime/CI 保存机械证据。

### Commit describes state

`evo-commit` 只记录已经理解和验证过的工程状态。默认不 Push；Goal 可预授权 `final-only` 或 `per-ticket`。Force push、protected/default branch、history rewrite、merge、tag、release、deploy 仍需单独明确授权。

## Standard workflow

```text
setup-matt-pocock-skills
        ↓
     evo-init
        ↓
grill-with-docs / domain-modeling / research
        ↓
      to-spec
        ↓
 evo-spec-review
        ↓
     to-tickets
        ↓
 evo-plan-review
        ↓
Human approves intent + execution envelope
        ↓
      evo-goal
        │
        ├─ evo-implement
        ├─ tdd when appropriate
        ├─ evo-verify
        ├─ evo-review
        ├─ diagnosing-bugs when needed
        ├─ evo-commit
        └─ next tracker frontier
        ↓
 full evo-verify
        ↓
  final evo-review
        ↓
    evo-finish
        ↓
    evo-commit
        ↓
 push only if authorized
```

`evo-test` 是**手工触发**的较完整测试/验收 Skill，不属于默认 Goal 生命周期。它会复用项目已有测试体系，并在条件允许时执行关键 User Journey。

需求中途变化：

```text
evo-change
→ update canonical Spec / tickets / ADR / docs
→ preserve unaffected work/evidence
→ invalidate only affected conformance assumptions
→ rerun affected review gates
→ recompute tracker frontier
→ resume evo-goal
```

## EVO-owned Skills

| Skill | Responsibility |
|---|---|
| `ask-evo` | 根据当前 Repository / Tracker / Gate 状态选择唯一下一步。 |
| `evo-init` | 深入理解项目结构、规范、现有能力和代表实现。 |
| `evo-advisor` | 提供 Repository-grounded 资深工程/架构建议。 |
| `evo-spec-review` | 在 Ticketing 前检查 canonical Spec 的 Repository Fit。 |
| `evo-plan-review` | 在执行前检查 canonical Ticket Graph 的 Repository Conformance。 |
| `evo-implement` | 按现有结构和能力实现一个 bounded reviewed ticket，不负责 Git delivery。 |
| `evo-change` | 需求变化时更新 canonical owners，并保留未受影响工作。 |
| `evo-verify` | 将 Acceptance 映射到实际执行的 `PASS / FAIL / UNVERIFIED` 证据。 |
| `evo-review` | Commit 前检查 Repository Conformance、Intent 与 Evidence。 |
| `evo-test` | 手工触发广度测试、关键用户流程和风险相关检查。 |
| `evo-goal` | 在 Execution Envelope 内持续消费 reviewed ready frontier。 |
| `evo-finish` | 最终收敛 Current Truth、docs/domain/ADR/Tracker。 |
| `evo-commit` | AI-readable Commit + 受控 Push。 |
| `evo-recover` | 从 Repository / Tracker / Git / Tests / CI 恢复上下文。 |

## Harness compatibility

EVO-owned Skills 使用可移植 `SKILL.md`，正文不绑定某一种 Harness 的调用语法：

- Codex：`agents/openai.yaml`
- OpenCode：`metadata.opencode/autoinvoke`
- Claude Code：`disable-model-invocation`

Skill-to-Skill 依赖按逻辑 Skill ID 表达，例如“apply `tdd`”，而不是写死 `/tdd` 或某个工具 API。

## Principles

- Repository > Chat
- Evidence > Claim
- Existing Pattern > Reinvent
- Reference Before Edit
- Capability Before Creation
- Planning Conforms Before Execution
- One Fact → One Owner
- Change > Rewrite
- Human Owns Meaning; Agent Owns Execution
- Tracker Owns Progress
- Commit Describes State
- Minimum Necessary Process
