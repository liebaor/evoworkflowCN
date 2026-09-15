# EVO Skill 契约

每个 EVO Skill 都是一项可复用的工程能力，而不是一张原则说明纸。

## 必须明确的边界

一个 Skill 应明确说明：

1. **Purpose**：唯一职责。
2. **Use when**：正向触发条件。
3. **Do not use when**：不能吸收的相邻职责。
4. **Read first / Preconditions**：行动前必须读取的 Repository 证据。
5. **Workflow**：可重复执行的步骤。
6. **Stop / Escalate**：何时超出本 Skill 权限并移交。
7. **Repository writes**：允许修改哪些 `.evo/` 或项目表面。
8. **Output**：下一位 Human/Agent 可以消费的结果。
9. **Final checks**：交棒前必须满足什么。

## 固定工作区

Skills 必须直接使用：

```text
.evo/project.md
.evo/context.md
.evo/goal.md
.evo/decisions/
.evo/specs/
.evo/plans/
.evo/research/
```

不要为 EVO 知识增加可配置替代路径。项目尚未采用该 Convention 时，路由到 `evo-setup`。

## 角色边界

- `evo-advisor` 负责建议，不负责实现。
- `evo-grill-with-docs` 解决重大决策；事实由 Agent 自己调查。
- `evo-research` 解决外部不确定性；Repository 内部事实优先本地读取。
- `evo-spec` 综合已经确定的 Intent，不承担尚未解决的产品访谈。
- `evo-plan` 生成 fresh-Agent 可独立执行的 Slices。
- `evo-implement` 实现一个 Slice；Intent 改变时必须升级，而不是偷偷改计划。
- `evo-tdd` 用行为测试驱动实现；`evo-verify` 在实现后证明 Acceptance。
- `evo-review` 默认只读。
- `evo-finish` 负责 Current Truth 收敛。
- `evo-goal` 对已准备好的 Plan 做连续编排。
- `evo-commit` 记录 Git 历史，只有授权后才能 Push。

## Goal 规则

Goal 可以调用/应用其他 Skill 的契约，但不能绕过它们的安全边界。重大决策仍属于 Human Authority。Worker 不能把自己的自我报告当成最终验收；必须依赖直接 Evidence，并在 Harness 支持时优先使用 fresh review context。

## Router 同步

任何 Skill 集合或流程变化，都必须同步更新 `ask-evo`、README、workflow 文档、eval 场景和 CI。
