---
name: evo-init
description: 理解一个已经采用 EVO 的 Repository，并填充固定的项目与领域知识。通常在 `evo-setup` 后首次使用，或 `project.md/context.md` 明显不完整时使用。不要因为新 Session 开始就重复 Init。
---

# EVO Init

## Preconditions
固定 `.evo/` 工作区已经存在；否则先用 `evo-setup`。

## Purpose
让一个全新的 Agent 不依赖 Chat 记忆，也能导航、构建、测试并扩展当前 Repository。

## Workflow
1. 读取项目说明、README/Current Docs、manifests/lockfiles、源码结构、代表性实现、Tests、CI/build、Git history、运行入口和 `.evo/decisions/`。
2. 当宿主工具比静态猜测更可靠时直接使用它们，例如 effective dependency graph、framework command、test discovery、Git history。
3. 将发现分类为 Confirmed / Inferred / Unknown。Unknown 只有会实质改变当前工作或风险时才阻塞。
4. 写入/更新 `.evo/project.md`：系统用途；已确认的重要技术栈/版本；模块地图；build/test/run 命令；真实入口/consumer path；代表性 Existing Pattern；重要 Current Docs/External Systems；已知约束和有意义的 Unknown。
5. 写入/更新 `.evo/context.md`：只记录领域词汇与稳定业务事实。
6. 若发现长期设计理由且当前没有 Owner，写入 `.evo/decisions/`；不要为了填目录凭空创造 Decision。

## Output
总结系统是什么、去哪里工作、如何验证变更、应该复用哪些 Pattern，以及仍有哪些重大事实未知。

## Final checks
一个 Fresh Agent 只读 `AGENTS.md + .evo/project.md + .evo/context.md`，就能找到其余相关 Repository 内容，而不需要用户重新解释基础结构。
