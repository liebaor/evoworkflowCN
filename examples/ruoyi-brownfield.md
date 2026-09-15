# RuoYi Brownfield 接入示例

## 1. Setup

安装 EVO Skills，然后运行 `evo-setup`。

如果 Repository 中已有 `docs/adr/`、RFC 或领域 `CONTEXT.md`，Setup 会把工程记忆迁移到：

```text
.evo/decisions/
.evo/specs/
.evo/context.md
```

并修复引用，不保留指回旧目录的永久映射。

API、部署、用户文档继续留在项目原本的 docs 体系。

## 2. Init

运行 `evo-init`。Agent 读取真实 RuoYi Repository、Maven/Node metadata、代表性模块、Tests、CI 和 Git。静态 metadata 不够时，可以直接使用项目工具，例如：

```bash
mvn help:effective-pom
mvn dependency:tree
```

发现写入 `.evo/project.md` 和 `.evo/context.md`，并标注 Confirmed / Inferred / Unknown。Unknown 只有与当前任务相关时才阻塞。

## 3. Feature

例如会议室功能：

```text
evo-grill-with-docs
→ evo-spec (.evo/specs/meeting-room.md)
→ evo-plan (.evo/plans/meeting-room.md)
```

之后可以逐 Slice 实现，也可以运行 `evo-goal` 连续完成整个已准备好的 Plan。TDD 驱动稳定行为 Seam，Verify 通过 RuoYi 实际 Tests/API/UI 路径证明 Acceptance。

## 4. Delivery

Full Verify + Review 后，由 `evo-finish` 收敛 Current Truth 和 Decisions，再由 `evo-commit` 写入面向结果的 Git 历史。只有获得授权后才 Push。
