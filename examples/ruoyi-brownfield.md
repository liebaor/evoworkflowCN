# RuoYi Brownfield example — EVOworkflow 2.0

场景：在已有 RuoYi-derived system 中新增 Supplier Management，同时避免建立平行架构。

## Adopt

```text
setup-matt-pocock-skills
→ evo-init
```

`evo-init` 应检查真实 checkout，并在 `docs/agents/repository.md` 记录：

- controller/service/mapper flow；
- permission annotation 和 menu/button permission naming；
- DataScope 或等价数据权限；
- pagination/response convention；
- transaction/error convention；
- Vue API/table/form layout；
- representative backend/frontend tests；
- build/test/typecheck commands；
- 可复用 Framework/Project Capability，例如 `BaseController`、`AjaxResult`、`SecurityUtils`、`@PreAuthorize`、`@Log`、dictionary/DataScope 等。

应指向真实文件，而不是复制源码正文。

## Plan

```text
grill-with-docs
→ to-spec
→ evo-spec-review
→ to-tickets
→ evo-plan-review
```

Spec Review 应明确“不新建与现有 RuoYi 平行的 response/pagination/auth abstraction”。Plan Review 应让每个可执行 Ticket 标明实际 Reference 和 Capability reuse。

一个合理的 Backend CRUD Ticket 可以表达：

```text
Module fit: existing business module
Reference: existing mature CRUD module
Strategy: EXTEND
Reuse:
- BaseController
- startPage()
- getDataTable()
- AjaxResult
- @PreAuthorize
- @Log / BusinessType
- existing Service / Mapper / XML conventions
New abstractions: None
```

## Execute one ticket

```text
evo-implement
```

修改前重新打开真实 reference，例如：

```text
Permission: EXTEND → <existing reference>
Pagination: REUSE → <existing reference>
Supplier module structure: EXTEND → <existing CRUD reference>
```

没有 Repository-based 原因时，新建 permission/data-scope/response/pagination mechanism 不可接受。

然后：

```text
evo-verify
→ evo-review
→ evo-commit
```

## Manual test

需要更广验收时手工调用：

```text
evo-test Supplier Management
```

若项目已有 Browser/E2E 或可交互应用环境，可模拟：

```text
login
→ open Supplier Management
→ create
→ search
→ edit
→ delete/disable
```

权限相关改动还应尝试 authorized + unauthorized path。Browser 环境不可用时必须标记相应 User Journey 为 `UNVERIFIED`，不能用 API PASS 冒充 UI PASS。

## Execute continuously

Spec/Tickets 与 Delivery Policy 获得批准后：

```text
evo-goal
```

Goal 连续消费 Ready Frontier，并自行处理普通 code/test/review failure；只有需求/风险边界变化时停止。

## Requirement changes halfway through

如果 Supplier deletion 从 hard-delete 改成 disable-only：

```text
evo-change
```

只更新 canonical Spec/Tickets，保留不受影响的 finished CRUD work，仅失效 deletion-specific Evidence/Conformance assumption。必要时重新运行受影响的 `evo-spec-review` / `evo-plan-review`，重算 Frontier 后继续 Goal。
