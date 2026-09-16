# EVOworkflow 2.0 Workflow

## First adoption

```text
install combined Matt + EVO Skills
        ↓
setup-matt-pocock-skills
        ↓
evo-init
        ↓
ask-evo
```

Matt setup 负责 Issue Tracker 与 Domain Document 配置；EVO Init 负责语义理解“这个 Repository 实际应该怎么扩展”。

## Planning

```text
grill-with-docs / domain-modeling / research / wayfinder
        ↓
to-spec
        ↓
evo-spec-review
        ↓
to-tickets
        ↓
evo-plan-review
```

EVO 不维护 `evo-spec`、`evo-plan`、`evo-research` 或 `evo-grill-with-docs` 的平行副本。

## One bounded delivery

```text
ticket / bounded task
        ↓
evo-implement
        ↓
evo-verify
        ↓
evo-review
        ↓
evo-commit
```

`evo-implement` 适合时使用上游 `tdd`；复杂 observed failure 使用 `diagnosing-bugs`。

## Continuous Goal

```text
approved Spec + conformance-reviewed ticket graph + Execution Envelope
        ↓
evo-goal
        │
        ├─ choose ready frontier ticket
        ├─ snapshot delivery base
        ├─ evo-implement
        ├─ evo-verify
        ├─ diagnose/fix/reverify ordinary failures
        ├─ evo-review
        ├─ evo-commit
        ├─ close/update ticket
        └─ recompute frontier
        ↓
full evo-verify
        ↓
final evo-review
        ↓
evo-finish
        ↓
final evo-commit
        ↓
push only if pre-authorized
```

普通 build/test/lint/review failure 属于执行工作，不是打断人的理由。只有产品含义/风险边界变化、缺少 credentials/production authority、破坏性操作、或诊断已经没有新 Evidence Path 时停止。

## Manual test

`evo-test` 只能由用户显式触发：

```text
evo-test <scope>
        ↓
reuse project-native checks/tests
        ↓
focused behavior + integration/API as relevant
        ↓
critical user journey when practical
        ↓
PASS / FAIL / UNVERIFIED
```

它不属于默认 Goal，也不会默认安装新的 Test Framework。

## Requirement change

```text
accepted intent changes
        ↓
evo-change
        ↓
RETAIN / REVISE / REMOVE / ADD
        ↓
update canonical Spec / tickets / ADR / docs
        ↓
invalidate only affected evidence/conformance assumptions
        ↓
rerun affected gates
        ↓
recompute frontier
        ↓
resume implementation or Goal
```

## Recovery

Fresh Session 从 standing instructions、Repository Guide、Domain/ADR config、Tracker source/comments、Git status/log/diff、tests/CI 和 current code 恢复。Chat history 只是 optional context，不是 authority。
