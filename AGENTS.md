# EVOworkflow 仓库说明

EVOworkflow 是一套以 Repository 为中心、由 Skills 驱动、采用固定项目知识目录的软件工程工作流。

## 核心模型

- Human：产品方向、重大取舍、授权与最终验收。
- Agent + EVO Skills：语义理解、工程推理、实现、诊断、Review 与连续执行。
- `.evo/`：唯一的 AI 工程知识工作区。
- 项目原生 tests/build/lint/runtime/CI：确定性证据。
- Git：时间线与交付历史。
- Harness：执行环境、Sandbox、工具、Subagent 与长时间运行能力。

## 固定项目约定

所有采用 EVO 的项目统一使用：

```text
.evo/
├── project.md
├── context.md
├── goal.md
├── decisions/
├── specs/
├── plans/
└── research/
```

不要为 EVO 自有知识引入替代目录或项目级路径映射。Brownfield 接入时，应把已有 ADR/Decision、Working Spec/RFC、Implementation Plan、Research 和领域 Context 迁移到该结构并更新引用。

API 文档、部署说明、用户/运维文档等正式项目文档仍保留在项目自己的文档体系。`.evo/` 管理的是 AI 工程记忆与工作产物，不接管所有文档。

## 工程原则

- Repository > Chat。
- Evidence > Claim。
- Existing Pattern > Reinvent。
- One Fact → One Owner。
- Change > Rewrite。
- Minimum Necessary Process。
- Human Authority > Agent Autonomy。
- EVO 知识位置遵循 Convention Over Discovery。
- Unknown 只有在不同答案会实质改变当前任务或风险时才阻塞。

## Skill 维护

每个面向用户的 Skill 都应明确：Use when、Do not use when、Read first、Workflow、Stop/Escalate、Output、Final checks。

中文版本地化规则：`SKILL.md` 的 Markdown 结构标题保持英文，并尽量与英文主仓使用相同标题（如 `Purpose`、`Read first`、`Workflow`、`Output`、`Boundary`）；`name`/Skill ID 保持英文；`description` 和正文说明使用中文。不要翻译 Skill 的结构标题。

标准 Skill 集合记录在 README 和 `docs/skill-contract.md`。任何 Skill 的新增、删除、改名或职责边界变化，都必须在同一次变更中同步 `ask-evo`、README、workflow 文档、evals 和 CI。

`evo-goal` 是 Skill 级编排，不是运行时：一个 Repository、一个 Active Goal、一个 Writer。它可以反复应用 Implement/TDD/Verify/Bug/Review/Commit 契约，但重大决策仍必须交给人。

`evo-commit` 只描述已存在的状态，不创造证据。Push 必须得到用户明确授权，或由 `.evo/goal.md` 明确设置 push 策略。默认永不 force-push。

完成 EVOworkflow 仓库变更前，确认 Skill 集合、Router、metadata、文档与验证工作流保持一致。
