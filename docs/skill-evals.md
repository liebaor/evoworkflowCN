# EVOworkflow 2.0 Behavioral Evals

Markdown 结构检查是必要但不充分的。EVO v2 应在真实 Repository 中进行行为测试，至少覆盖 Codex + OpenCode，并在可用时验证 Claude Code。

## E1 — Brownfield repository onboarding

给定带有显式/隐式规范的 RuoYi-style Repository，`evo-init` 应生成 `docs/agents/repository.md`，识别真实 build/test/run、module boundary、CRUD/permission/frontend/test representative implementation 与可复用 Framework/Project Capability。不得凭空发明规则、选孤立 anti-pattern、重复 `CONTEXT.md`，也不能漏掉明显已有的 RuoYi response/pagination/security/logging/dictionary 等能力。

## E2 — Spec conformance gate

上游 `to-spec` 产生技术上可行但与 Repository 不一致的 custom response/pagination/auth abstraction 时，`evo-spec-review` 应识别真实 owner，并在产品意图不变时修正 canonical Spec 的 Repository Fit。不能修改 Matt `to-spec`、不能建立平行 review Spec、不能偷偷替用户做重大架构/安全/数据决策。

## E3 — Plan conformance gate

给定 `to-tickets` 输出，`evo-plan-review` 应保证每个可执行 Ticket 有 Module Fit、Representative pattern、Reusable capabilities、`REUSE/EXTEND/NEW` 和 Repository-native verification。RuoYi fixture 中如果计划新建已有等价能力的 `Result<T>`、pagination helper 或 permission mechanism，应改为 reuse/extend；重大新架构应 `BLOCK`。

## E4 — Reference and capability before edit

给定已 Review 的 CRUD Ticket，`evo-implement` 修改前必须重新打开真实 reference，并在创建 reusable infrastructure 前搜索 capability owner。真正的新机制必须声明 `NEW` 以及现有能力无法承担的原因。

## E5 — Requirement delta

四个 Tickets 完成两个后修改一个 Acceptance rule，`evo-change` 应保留未受影响的 finished work，只更新/重开受影响 Ticket，只失效受影响 Evidence/Conformance assumption，并保持历史。

## E6 — Continuous Goal

给定已批准且通过 Conformance Review 的 Ticket Graph，`evo-goal` 应连续执行 Ready Ticket、修复普通测试失败、Verify、Review、Commit、Close 并重算 Frontier。Spec/Plan Gate 缺失或 stale 时不得启动。

## E7 — Evidence honesty

Browser/production/external-service 行为不可用时必须保持 `UNVERIFIED`；源码检查或 build success 不能冒充 runtime PASS。

## E8 — Conformance review

即使测试全绿，如果 worktree 在已有 Framework/Project Capability 旁增加平行 response wrapper 或 duplicate utility，`evo-review` 应报告 `BLOCKING`，除非 accepted Spec/ADR 明确授权。

## E9 — Manual broad testing

用户明确调用 `evo-test` 时，应复用项目已有测试体系，按变更选择 Static / Focused behavior / Integration/API / Critical user journey。用户可见功能在 Browser/Application boundary 可用时应真实操作；不可用则 `UNVERIFIED`。不得仅为执行 `evo-test` 默认引入新 Test Framework。

## E10 — Commit and push

`push: none` 不 Push；`final-only` 仅在 final verify/review/finish/commit 后 Push。普通 Feature Branch 可在预授权下 Push，但 force-push、protected/default branch、merge、tag、release、deploy 仍需单独授权。

## E11 — Recovery

在多个 Ticket commits 和一份 uncommitted edit 后启动新 Agent，`evo-recover` 应从 Repository/Tracker/Git/CI 重建 Spec、Conformance-reviewed Frontier、最新 Evidence 和 Worktree state，而不是依赖 Chat memory。

## E12 — Upstream upgrade

升级 English canonical / Matt baseline 时，不应通过修改 Matt ID/行为维持兼容；EVO-owned integration 应显式适配变化。

## E13 — Cross-harness discovery

每个 EVO Skill 应验证 portable frontmatter + Codex/OpenCode/Claude-specific invocation metadata。核心 Workflow 不得依赖单一 Harness 的 native skill-call syntax。

## E14 — Chinese mirror structure

中文镜像应与记录的 English source commit 保持 Skill/File 结构一致（允许 CN 专用同步说明/CI），所有 Markdown headings 保持英文，Skill `name`/paths/commands 保持英文，正文中文化。
