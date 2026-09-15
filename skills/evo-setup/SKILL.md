---
name: evo-setup
description: 让 Repository 正式采用 EVO：建立固定 `.evo/` 工作区，并把已有工程知识迁移进去。适用于项目第一次接入 EVO，或当前 EVO 工作区结构不完整的情况。
---

# EVO Setup

## 目的
在任何长期工作流依赖工程知识前，先让知识位置确定下来。

## 何时使用
- `.evo/` 缺失或不完整；
- Brownfield 项目首次接入 EVO；
- 旧 ADR/RFC/Spec/Plan/Context 分散在多个位置。

## 不要用于
- 工作区已经正常，只是还不了解项目 → `evo-init`；
- 新 Session 只是丢了上下文 → `evo-recover`。

## 固定目录

```text
.evo/project.md
.evo/context.md
.evo/goal.md        # 仅开始 Goal 时创建
.evo/decisions/
.evo/specs/
.evo/plans/
.evo/research/
```

## 流程
1. 探索 `AGENTS.md`/项目说明、领域 Context/Glossary、ADR/Decision、Working Spec/RFC/Design、Implementation Plan、Research Notes 及其引用关系。
2. 按职责而不是文件名分类。
3. 迁移 EVO 自有工程知识：Durable rationale/ADR → `decisions/`；未完成 Spec/RFC/Proposal → `specs/`；可执行 Plan → `plans/`；外部 Research → `research/`；稳定领域语言/事实 → 合并到 `context.md`。
4. 尽量使用 Git-aware move，保留历史并更新 Markdown/源码引用。
5. API、部署、用户/运维等正式项目文档留在原 Docs 体系。
6. 创建最小 `.evo/project.md`，指向下一步 `evo-init`。
7. 在 `AGENTS.md` 中加入简短说明：Agent 先读 `.evo/project.md`，并遵循固定工作区。
8. 搜索迁移后失效的旧引用并修复。

## 模糊情况
不保留永久路径映射。若一个文档同时包含 Current Documentation 和 Decision rationale，保留 Current Documentation 原位，把长期 rationale 提取/迁移到 `.evo/decisions/`。只有当分类会实质改变文档 Owner 时才询问人。

## 输出
报告新建目录、已迁移产物、已更新引用、明确留在 `.evo/` 之外的文档，以及未解决分类。

## 最终检查
已迁移工程知识只有一个 Canonical Owner；旧 ADR/Spec/Plan/Context 位置不能继续作为竞争 Owner。
