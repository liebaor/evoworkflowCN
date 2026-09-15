# EVOworkflow 工作模型

## 项目接入

```text
安装 Skills
→ evo-setup
→ evo-init
→ ask-evo
```

`evo-setup` 建立固定工作区并迁移 Brownfield 工程记忆；`evo-init` 再学习真实代码库并填充 Project/Context 知识。

## 标准功能路线

```text
按需 advisor / grill / research
→ spec
→ plan
→ implement（适合时使用 tdd）
→ verify
→ review
→ finish
→ commit [→ 授权后 push]
```

## 长时间执行路线

Spec 和 Plan 准备好后：

```text
evo-goal
  对每个 slice 循环：
    implement
    适合时 tdd
    focused verify
    失败则 fix 或 bug loop
    策略允许时 checkpoint commit
  全部完成后：
    full verify
    independent review
    finish
    final commit
    optional push
```

普通代码/测试失败只要 Agent 还能获得新证据并继续，就不应停止 Goal。遇到重大人类决策、缺少授权/凭据、破坏性不可逆操作、目标互相矛盾，或反复失败且已经没有新的诊断路径时才停止。

## TDD

TDD 是实现方法，不是最终 Acceptance 证明：

1. 选择一个公开行为 seam；
2. 先写一个聚焦测试；
3. 运行测试，确认失败原因确实是目标行为缺失/错误；
4. 写最小实现使其变绿；
5. 运行该测试和附近 Regression；
6. 只在绿色状态下做不改变行为的 Refactor；
7. 一次推进一个 vertical slice。

避免一次写完全部测试的横向切片，以及与实现细节强耦合的断言。

## Review 与 Finish

Review 独立回答三个问题：

- **Intent**：是否真正实现用户要求的 Outcome？
- **Engineering**：是否安全、可维护，并符合当前 Repository？
- **Evidence**：实际执行过的检查是否足以支持结论？

Finish 再让 Current Docs、`.evo/context.md`、Durable Decisions、Working Specs/Plans 与 Goal Progress 收敛，使下一个 Agent 读到一致的 Repository。

## Delivery

Commit 是交付历史步骤。它读取 Diff 与已验证上下文，写出 AI 可读的 Commit Message。Push 必须显式授权，绝不默认发生。
