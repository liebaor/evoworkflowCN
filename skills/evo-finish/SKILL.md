---
name: evo-finish
description: 把已经 Verify 和 Review 的工作收敛成一致的 Repository Current Truth。Implementation 通过所需验证与复核后、最终 Commit/Delivery 前使用。
---

# EVO Finish

## Preconditions
Required Acceptance 已 PASS，或责任人明确接受 UNVERIFIED；Blocking Review Findings 已解决。

## Read first
`.evo/project.md`、`.evo/context.md`、Active 时的 `.evo/goal.md`、Owning Spec/Plan、相关 Decisions、Diff、Current Project Docs、Verification/Review Results。

## Workflow
1. Shipped Behavior 改变时更新 Current Project Docs/Contracts。
2. 只把稳定领域 Fact/Vocabulary 更新到 `.evo/context.md`。
3. 对应该长期保留、能超越 Working Spec 的 Rationale 创建/更新 `.evo/decisions/`。
4. 清除陈旧 Future-tense Claim，并让 Working Spec/Plan 与实际 Shipped 内容一致。其唯一长期信息已被 Decisions/Current Docs/Goal 吸收后，可删除 Working Artifact；Git 保存历史。
5. Navigation、Module、Command 或稳定 Entry Path 改变时更新 `.evo/project.md`。
6. 当前 Goal 完成时，把 `.evo/goal.md` 标记 COMPLETE，并写最终 Evidence Summary 与 Remaining Accepted Limitations。
7. 清理 Spec/Plan 后检查所有引用/链接。

## Boundary
Finish 不创造缺失 Evidence、不做 Code Review，也不宣称 Git Delivery 已发生。

## Output
报告修改的 Current-Truth Surface、保留的 Durable Decisions、删除/保留的 Working Artifacts，以及有意留下的未解决项。随后路由到 `evo-commit`。
