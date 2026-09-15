---
name: evo-recover
description: 从固定 `.evo/` 工作区、Git 和当前 Repository Evidence，为 Fresh/Interrupted Agent 或 Session 重建已有 EVO 工作上下文。已有工作但 Chat Context 丢失时使用；不要用于第一次接入项目。
---

# EVO Recover

## 读取顺序
1. `AGENTS.md` 和 `.evo/project.md`。
2. `.evo/context.md`。
3. 存在时的 `.evo/goal.md`，并跟随其中 Spec/Plan 链接。
4. 相关 `.evo/decisions/` 和 Research。
5. Git branch/status/recent commits/diff。
6. 当前 Slice 周围的 Source/Tests 和可用 CI Results。

## 重建
确定 Objective/Non-goals、当前/最近 Goal Status、Completed vs Pending Slices、Last Verified Evidence、相关 Decisions/Patterns、Changed Files、Likely Next Seam 和 Material Blockers。

Repository Evidence 优先于陈旧 Chat Summary。Progress Checkbox 没有对应 Git/Evidence 时不能当作 Proof。

## 输出
生成紧凑 Handoff：Objective；Active Canonical Artifacts；实际 Completed/Verified；Pending；Blockers/Unknowns；唯一下一 EVO Skill。

除非用户明确要求，否则不开始实现。
