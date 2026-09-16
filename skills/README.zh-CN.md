# EVOworkflow 2.0 Skills

本仓库是英文 EVOworkflow 的中文镜像，包含 **Matt Skills 中文翻译 + EVO Extensions 中文翻译**。Skill ID、目录、命令、代码标识和机器字段保持英文；自然语言正文中文化；Markdown headings 保持英文。

## Installation

```sh
npx skills@latest add liebaor/evoworkflowCN
```

不要在同一目标重复安装英文 EVOworkflow 或 `mattpocock/skills`，避免重复 Skill ID。

## Matt upstream

当前 Matt upstream commit：

`959a8e9f1edc3adbe2f7e3054bb6fbefa6696260`

共 25 个正式 Engineering + Productivity Skills。中文仓库会翻译 Matt 的 Skill 正文和辅助说明，但保持原始 Skill name、文件结构和工程语义。

## EVO-owned

| Skill | Responsibility |
|---|---|
| `ask-evo` | 根据 Repository / Tracker / Gate 状态选择唯一下一步。 |
| `evo-init` | 理解项目规范、架构、命令、reference 和 reusable capability。 |
| `evo-advisor` | Repository-grounded 高级工程/架构建议。 |
| `evo-spec-review` | `to-spec` 后检查方案层 Repository Fit。 |
| `evo-plan-review` | `to-tickets` 后检查 Ticket 的 Module/Reference/Reuse/Verification Fit。 |
| `evo-implement` | 按现有结构和能力实现 bounded reviewed ticket。 |
| `evo-change` | 需求变化时更新 canonical owners 并保留未受影响工作。 |
| `evo-verify` | Acceptance → `PASS / FAIL / UNVERIFIED`。 |
| `evo-review` | Commit 前检查 Repository Conformance、Intent、Evidence。 |
| `evo-test` | 手工触发较完整测试和关键 User Journey。 |
| `evo-goal` | 在 Execution Envelope 内连续完成 reviewed ready frontier。 |
| `evo-finish` | 完成后的 Current Truth convergence。 |
| `evo-commit` | 结构化 Commit + 受控 Push。 |
| `evo-recover` | 从 Repository / Tracker / Git / CI 恢复 Session。 |

## Core workflow

```text
to-spec
→ evo-spec-review
→ to-tickets
→ evo-plan-review
→ evo-goal / evo-implement
```

开发约束：

- **Reference Before Edit**
- **Capability Before Creation**
- **Planning Conforms Before Execution**

对于 RuoYi 等 Brownfield 项目：`current Repository usage > generic framework tutorial > AI-preferred new abstraction`。

`evo-test` 是额外手工能力，不会自动加入 `evo-goal`。
