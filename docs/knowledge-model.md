# Repository knowledge model

EVOworkflow 2.0 遵循 **One Fact → One Owner**，复用 Repository 已有知识系统，不把所有内容搬进 EVO 专属目录。

| Question | Primary owner |
|---|---|
| 项目长期 Agent 指令是什么？ | `AGENTS.md` / existing host instruction root |
| Domain term 是什么意思？ | `CONTEXT.md` 或 Matt setup 配置的布局 |
| 为什么做了一个 durable technical choice？ | Matt setup 配置的 ADR |
| 这个 Change 应该实现什么？ | canonical Spec / parent issue |
| 还剩什么工作、谁阻塞谁？ | configured Issue Tracker / local ticket files |
| Repository 怎么组织，新代码应该像谁？ | `docs/agents/repository.md` + linked authorities/source |
| 产品现在真实做什么？ | Source / contracts / current product docs |
| 什么证明行为正确？ | Tests / runtime observation / CI / durable verification notes |
| 历史发生了什么？ | Git / PR / Tracker history |

## Repository guide

`evo-init` 创建/刷新 `docs/agents/repository.md`，包含指针和简洁结论：

- authority documents；
- build/test/run commands；
- architecture/module boundaries；
- representative consumer paths；
- reusable framework/project capabilities；
- reference implementations by concern；
- known inconsistencies / meaningful unknowns。

它不能复制整份 coding standards、domain glossary、ADR rationale 或 source code。

## Conformance ownership

Canonical Spec 自己拥有方案层 `Repository Fit`；canonical Ticket 自己拥有执行层的 Module Fit、Reference、Capability reuse、`REUSE/EXTEND/NEW` 和 verification approach。`evo-spec-review` / `evo-plan-review` 修改真正 owner，不创建旁路 Review 文档。

## Tracker owns progress

Ticket status、dependencies、claims、completion 只存在一个 Tracker。Goal 从真实 Tracker 重算 Frontier，而不是在其他文件镜像 `[x]`。

Execution Envelope 可以简洁地持久化在 Parent Spec/Task，供新 Session 恢复 delivery policy，但不能变成第二套工作流数据库。

## Knowledge convergence

`evo-finish` 在最终 Evidence/Review 后进行 knowledge gardening：只有 shipped behavior 真正改变时才更新 current docs、domain language、ADR；同时 reconcile Tracker artifacts，清理过期 future-tense claims。Git 保留历史。
