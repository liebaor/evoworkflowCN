# EVO Skill Contract

EVO 2.0 Skills 是围绕 Matt upstream 的集成契约。中文镜像翻译人类可读内容，但保持英文 canonical source 的 Skill IDs、结构、机器字段和工作流语义。

## Portable Skill shape

每个 EVO Skill 必须：

1. directory / `name` 使用 lowercase kebab-case；
2. 提供清晰的中文 trigger-oriented `description`；
3. 提供 `compatibility`，但不假设单一 Harness API；
4. portable behavior 放在 `SKILL.md`；
5. Codex policy 放在 `agents/openai.yaml`；
6. OpenCode invocation policy 使用 `metadata.opencode/autoinvoke`；
7. Claude Code user-invocation policy 使用 `disable-model-invocation`；
8. 引用上游能力时使用 Skill ID，不写 `/command` 或 tool-call syntax。

## Translation shape

- 所有 Markdown headings 使用英文。
- Frontmatter key、Skill name、路径、命令、代码/API identifier 保持英文。
- `description` 和自然语言正文中文化。
- UI `display_name` 视为标题，保持英文；`short_description` 中文化。
- 法律文本不替换原文。

## Upstream capability dependency

EVO Skill 需要 Matt capability 时：

- 优先使用当前 Harness 的 installed-Skill mechanism；
- 不修改/覆盖同名 Matt Skill；
- 必需能力不可用时返回 `MATT_SKILL_REQUIRED: <skill-id>`；
- optional capability 不可用时，只执行更窄的 EVO 行为，并明确说明未应用的部分。

## Repository-conformance contract

Planning 与 implementation 都必须使用同一份 Repository Contract：

- `evo-spec-review`：方案层确认 Architecture/Framework Fit；
- `evo-plan-review`：每个 Ticket 确认 Module Fit、Representative pattern、Reusable capability、`REUSE/EXTEND/NEW`、Verification fit；
- `evo-implement`：真正修改前重新打开 reference 和 capability owner；
- `evo-review`：阻止没有授权的 parallel/duplicate abstraction。

两个 standing rules：

- **Reference Before Edit**
- **Capability Before Creation**

## Evidence contract

Acceptance claim 只有三种状态：

- `PASS`：直接证据已实际执行/观察，并支持 claim；
- `FAIL`：直接证据与 claim 冲突；
- `UNVERIFIED`：所需直接证据不可用或未运行。

静态源码检查不能证明 runtime behavior；build/lint 只证明对应工具真正检查的规则。

## Manual test contract

`evo-test` 只能显式手工调用。它可以选择 Static、Focused behavior、Integration/API、Critical user journey 和风险相关检查，但不会为了满足流程默认安装新的 Test Framework。Browser/Application/External boundary 无法实际执行时必须 `UNVERIFIED`。

## Git contract

Commit 位于 implementation/evidence/review 下游。默认 **no push**。Goal 可以持久化 `final-only` / `per-ticket` 授权；Force push、history rewrite、protected/default branch、merge、tag、release、deploy 需要单独授权。
