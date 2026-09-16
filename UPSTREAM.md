# Upstream policy

本仓库是 EVOworkflow 英文 canonical repository 的中文镜像，同时包含 Matt Pocock Skills 的中文翻译。

## Source

- Canonical repository: `liebaor/evoworkflow`
- Canonical source ref for this sync: `v2/conformance-gates`
- Canonical source commit: `4de1c787712ed89b2934101055b871e5691b19f9`
- Matt repository: `mattpocock/skills`
- Matt upstream commit: `959a8e9f1edc3adbe2f7e3054bb6fbefa6696260`
- Matt imported scope: formal Engineering + Productivity Skills
- Matt Skill count: 25
- EVO-owned Skill count: 14
- Matt license: MIT，原文保留在 `THIRD_PARTY_LICENSES/mattpocock-skills-LICENSE`

## Mirror rule

1. English EVOworkflow 是结构和行为的 canonical source。
2. 中文仓库保持相同 Skill ID、目录、命令、路径、代码标识和机器字段。
3. 面向人的正文、`description`、说明文本翻译为中文；Markdown headings 保持英文。
4. Matt 中文版是 translation mirror，不可能与英文 Matt tree SHA 相同，因此 CN CI 不使用 byte-level tree equality。
5. 中文化不得改变工作流语义；如果需要行为变化，应先修改英文 canonical repository，再同步到中文仓库。
6. 法律文本保留原文；代码执行逻辑保持原样。

## Matt capabilities

Engineering Skills：

- `ask-matt`
- `code-review`
- `codebase-design`
- `diagnosing-bugs`
- `domain-modeling`
- `grill-with-docs`
- `implement`
- `improve-codebase-architecture`
- `prototype`
- `research`
- `resolving-merge-conflicts`
- `setup-matt-pocock-skills`
- `tdd`
- `to-spec`
- `to-tickets`
- `triage`
- `wayfinder`
- `wizard`

Productivity Skills：

- `grill-me`
- `grilling`
- `handoff`
- `teach`
- `to-questionnaire`
- `wait-what`
- `writing-for-agents`

## Sync procedure

英文仓库更新后：

1. 对比 English canonical source 与本仓库的文件清单。
2. 新增/删除/移动文件，使结构一致（中文专用 CI/说明除外）。
3. 翻译变化的自然语言内容，同时保持 headings、IDs、paths、commands 和 code semantics。
4. 更新本文件中的 canonical source commit。
5. 检查 25 个 Matt Skill + 当前 EVO-owned Skill 清单完整。
6. 运行 CN CI：Skill metadata、英文 headings、retired Skill、不允许 `.evo/` Runtime 等检查。
7. 只有在结构与语义同步后才接受新的中文镜像基线。
