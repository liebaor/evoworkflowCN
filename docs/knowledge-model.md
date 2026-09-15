# EVO Repository 知识模型

EVO 使用固定 `.evo/` 工作区，让每个 Agent 都知道工程记忆在哪里，不需要重新发现。

## 唯一 Owner

| 问题 | 唯一 Owner |
|---|---|
| 这个项目是什么，如何导航/build/test/run？ | `.evo/project.md` |
| 领域术语和稳定业务事实是什么意思？ | `.evo/context.md` |
| 为什么做出一个长期技术/架构选择？ | `.evo/decisions/` |
| 我们正在创建什么尚未完成的行为/设计？ | `.evo/specs/` |
| 哪些 bounded slices 执行这项工作？ | `.evo/plans/` |
| 哪些最新外部知识支持当前选择？ | `.evo/research/` |
| 当前正在连续执行什么目标？ | `.evo/goal.md` |
| 产品当前实际暴露什么？ | 项目源码 / contracts / current docs |
| 什么可以机械证明行为？ | 项目 tests / runtime / CI |
| 历史发生过什么？ | Git / PR history |

## Brownfield 迁移

EVO 不为旧的工程记忆目录保留路径映射。`evo-setup` 会把已有 ADR/Decision、Working Spec/RFC、Implementation Plan、Research 和领域 Context 迁移到固定位置并更新引用。

不要因为文档包含技术内容就全部迁移。API Reference、部署说明、用户/运维指南、当前公开架构文档继续保留为项目文档。如果其中包含长期 Decision rationale，则提取该理由到 `.evo/decisions/`，Current-State 文档仍留在原位置。

## One fact, one owner

避免维护多个可变副本。当前行为属于源码/contracts/current docs；理由属于 Decisions；未完成目标属于 Specs；执行拆分属于 Plans；外部证据属于 Research。

## Goal 不是隐藏状态

`.evo/goal.md` 必须保持可读，可包含 Objective、Spec/Plan 链接、Execution Policy、Progress、Current Slice、最近 Verify 结果和 Blocker。它是执行产物，不是机器专用状态库。

一个 checkout 最多只有一个 Active Goal。Goal 完成后可以保留，直到下一个 Goal 覆盖；历史由 Git 保存。

## Fresh-session 规则

一个全新的 Agent 应能通过读取 `AGENTS.md`、`.evo/project.md`、`.evo/context.md`、必要时的 `.evo/goal.md`、关联 Spec/Plan/Decisions、Git diff/history 以及当前 Tests/CI 证据恢复工作上下文。
