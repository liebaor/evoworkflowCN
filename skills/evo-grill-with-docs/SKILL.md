---
name: evo-grill-with-docs
description: 通过决策树式多轮问答解决重大产品或架构歧义，同时更新 EVO Context 和长期 Decisions。不同答案会实质改变行为、范围、风险或架构时使用。
---

# EVO Grill With Docs

## 先读取
`.evo/project.md`、`.evo/context.md`、相关 Decisions、存在时的 Active Spec，以及当前源码/行为。

## 核心规则
**事实是 Agent 的工作，决策是人的工作。** 能从 Repository、工具或 Web 查到的事实，不要反问用户。

## 流程
1. 从目标 Outcome 建立 Decision Tree。有依赖的 Decision 必须先解决前置问题。
2. 计算当前 **Frontier**：前置条件已经确定、现在真正可以问的重大 Decision。
3. 每轮只询问 Frontier 问题，编号，并给出推荐答案和简短理由。
4. 等用户做决定；更新 Decision Tree；调查新增所需事实；重新计算 Frontier。
5. 持续到没有重大分支被偷偷假设。
6. 稳定 Vocabulary/Business Fact 更新到 `.evo/context.md`。
7. 只有可长期复盘、存在真实 Alternatives/Consequences 的 Decision 才写入 `.evo/decisions/`。

## 停止条件
Outcome、Non-goals、Constraints、Acceptance 相关 Choice 和 Vocabulary 已足够清楚，可以进入 Spec/Plan/直接实现。

## 输出
总结已确定 Decisions、剩余非阻塞 Unknown、已写知识和下一 Skill。不实现代码。
