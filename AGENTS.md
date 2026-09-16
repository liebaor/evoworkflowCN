# EVOworkflow repository instructions

EVOworkflowCN 2.0 是英文 canonical repository 的中文镜像。目录、Skill ID、机器字段和行为契约必须与英文源保持一致；自然语言正文翻译为中文，Markdown headings 保持英文。

## Architectural invariants

- 英文 `liebaor/evoworkflow` 是 canonical source；当前同步 commit 记录在 `UPSTREAM.md`。
- Matt Skills 在英文仓库中作为 vendored upstream；中文仓库翻译其人类可读内容，但不得改变 Skill ID、目录结构、命令和工程语义。
- 不得用同名 Skill 覆盖 Matt；行为差异必须放到独立 `evo-*` Skill。
- EVO 2.0 不使用中央 Runtime、CLI 状态机、`.evo/state.yml`、阶段数据库或重复的 Tracker Progress。
- Issue Tracker 拥有 Spec/Ticket Progress 和 Blocking 关系。
- Source/contracts/current docs 拥有当前行为；`CONTEXT.md` 拥有 domain vocabulary；ADR 拥有 durable rationale；Git/PR 拥有 chronology；tests/runtime/CI 拥有 mechanical evidence。
- `docs/agents/repository.md` 是 authorities、结构、命令、reusable capabilities 和 representative implementations 的地图，不是复制百科全书。
- **Reference Before Edit**：非机械实现前找最近的现有 Pattern，并分类 `REUSE / EXTEND / NEW`。
- **Capability Before Creation**：新建公共 Utility/Component/Base abstraction/Framework-like mechanism 前，先证明 Repository/Framework 没有合适 owner。
- Spec/Ticket 在进入 `evo-goal` 前必须通过 `evo-spec-review` 与 `evo-plan-review`。
- 人负责产品含义、重大决策、风险接受和外部授权；Agent 可在批准的 Execution Envelope 内连续执行机械转换。
- Commit 只描述状态，不创造 Acceptance 或 Completion。
- `evo-test` 只能手工触发，不能隐式加入默认 Goal 生命周期。

## Translation contract

- Markdown H1/H2/H3 等 headings 保持英文。
- Skill directory、frontmatter `name`、metadata key、文件路径、命令、代码标识、协议/API 字段保持英文。
- `description`、说明段落、表格说明、提示语等自然语言翻译为中文。
- `agents/openai.yaml` 的 `display_name` 作为 UI 标题保持英文；`short_description` 可中文化。
- Shell/代码逻辑保持原样；仅翻译注释和面向人的输出文本，且不得改变行为。
- MIT License 等法律文本保留原文，不做翻译替代。

## Cross-harness contract

EVO-owned Skill 的通用行为放在 `SKILL.md`，不得在正文绑定某一 Harness 的 tool-call 语法。

每个 EVO-owned Skill 必须：

- 使用与目录一致的 lowercase kebab-case `name`；
- 提供中文 `description` 和兼容性说明；
- Claude Code user-invoked Skill 保留 `disable-model-invocation: true`；
- OpenCode 使用 `metadata.opencode/autoinvoke: "false"`；
- Codex 使用 `agents/openai.yaml`，并保持 `policy.allow_implicit_invocation: false`；
- 引用 Matt capability 时使用逻辑 Skill ID，不写死 slash command/tool syntax；
- 必需的 Matt capability 不可用时返回 `MATT_SKILL_REQUIRED: <id>`，不得静默复制另一套实现。

## EVO-owned Skill set

`ask-evo`, `evo-init`, `evo-advisor`, `evo-spec-review`, `evo-plan-review`, `evo-implement`, `evo-change`, `evo-verify`, `evo-review`, `evo-test`, `evo-goal`, `evo-finish`, `evo-commit`, `evo-recover`。

## Sync discipline

同步英文仓库时：

1. 记录新的 English source commit。
2. 对齐目录和 Skill 清单。
3. 翻译新增/变化的人类可读内容。
4. 保持 headings / IDs / machine fields 约定。
5. 更新 CN CI 和 Evals。
6. 不因翻译而引入新的工作流语义。
