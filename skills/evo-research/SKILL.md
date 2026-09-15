---
name: evo-research
description: 使用高可信 Primary Sources 解决最新外部技术不确定性，并把可复用结论保存到 `.evo/research/`。适用于当前 API、版本、标准、上游行为、技术对比和外部方案证据；Repository 内已有答案时不要使用。
---

# EVO Research

## Read first
`.evo/project.md`、`.evo/context.md`、相关 Decisions/Spec 和具体问题。

## Workflow
1. 明确 Decision/Question 和 Repository 约束。
2. 优先检索当前 Primary Sources：官方文档、标准、上游 Repository/Release、权威论文、原始 Change/Issue。
3. 社区讨论主要用于经验信号，不作为唯一事实来源。
4. 只比较真实可行替代方案，关注 Compatibility、Maintenance、Migration、Operational Risk、Lock-in、Maturity、Evidence Quality。
5. Freshness 重要时明确日期/版本。
6. 如果结论值得跨 Chat 复用，写 `.evo/research/<topic>.md`，包含日期、问题、已验证外部事实和引用/链接、对当前 Repository 的影响、建议和未解决不确定性。

## Boundary
Research 提供决策依据，不代表自动授权重大取舍；重大取舍应通过 Grill/Spec/Change 交给人。

## Output
先给 Answer/Recommendation 与 Evidence Quality，再说明对 Repository 的影响和下一 Skill。
