# EVOworkflow 2.0 Architecture

## Positioning

EVOworkflow 是 Matt Pocock Skills 之上的扩展层，不是 Matt 的行为 Fork，也不是 Agent Runtime。英文仓库携带固定版本的 Matt Skills；中文仓库同步同样结构并翻译人类可读内容。

```text
Human
  │ owns intent, material decisions, risk, external authorization
  ▼
Matt engineering methods + EVO extension contracts
  │
  ├── Repository / CONTEXT / ADR / current docs
  ├── Issue tracker (specs, tickets, dependencies, progress)
  ├── Source / tests / runtime / CI
  └── Git / PR history
```

不存在 `.evo/` 状态数据库。

## Responsibility split

### Matt upstream

提供成熟的软件工程方法：domain modeling、grilling、research、Spec synthesis、tracer-bullet ticketing、TDD、bug diagnosis、codebase design、wayfinding、code review 以及 supporting productivity Skills。

中文仓库翻译这些 Skill 的人类可读说明，但保留 ID、结构、调用关系与工程语义。

### EVO extensions

EVO 只解决长期项目中的集成问题：

- semantic repository onboarding 和 repository conformance；
- Spec/Plan conformance gates；
- changed-intent propagation；
- acceptance-to-evidence verification；
- pre-delivery worktree review；
- manual broad testing / user journey；
- continuous ticket-frontier execution；
- current-truth convergence；
- cross-session recovery；
- structured commit 和 authorized push policy。

## Execution Envelope

Goal 只有在意图和边界足够明确后才可连续执行。Envelope 至少包含：

- source Spec / parent task；
- tracker scope/frontier；
- commit policy；
- push policy（`none` / `final-only` / `per-ticket`）；
- human-stop conditions。

Envelope 应存在 canonical tracker source/local tracker document 上，而不是第二个进度数据库。

## Repository conformance

实现形态遵循：

```text
Human-approved intent (WHAT)
        ↓
Documented repository rules (HOW constraints)
        ↓
Representative existing implementation (SHAPE)
        ↓
Existing repository/framework capability
        ↓
Matt/general engineering heuristics (FALLBACK)
```

文档规范与真实 dominant implementation 冲突时，明确记录冲突，不要偷偷选择方便的一方。

## Planning gates

Matt `to-spec` / `to-tickets` 保持原始方法，EVO 在其后增加：

```text
to-spec
→ evo-spec-review
→ to-tickets
→ evo-plan-review
→ evo-goal
```

Spec Review 关注架构/Framework Fit；Plan Review 关注可执行 Ticket 是否复用现有模块、Pattern、Capability 与验证方式。

## No hidden orchestration runtime

`evo-goal` 是 Skill-level orchestrator。它从 Tracker、Git 和 Evidence 推导进度，不维护 locks、phase state、fingerprints、adapters 或重复 Slice ledger。

`evo-test` 是人工触发的额外测试能力，不会成为隐藏的 Goal 阶段。
