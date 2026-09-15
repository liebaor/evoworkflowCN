---
name: evo-tdd
description: 用有效 RED、最小 GREEN 和安全 REFACTOR 以 Test-first 方式推进一个行为。用户要求 TDD/Test-first，或计划 Slice 有稳定行为 Seam 值得自动化锁定时使用。
---

# EVO TDD

## 目的
让测试驱动行为实现，而不是在代码写完后装饰测试。

## 先读取
`.evo/project.md`、`.evo/context.md`、当前 Spec/Plan Acceptance、相关 Decisions 和目标 Public Seam 周围的 Existing Tests。

## 选择 Seam
通过最高层、稳定且能给出有用反馈的 Public Interface 测行为。优先已有 Seam 和项目测试约定。避免测试 Private Method/Internal Collaborator Choreography，除非它本身就是 Public Contract。

## 循环
1. **One behavior**：选择一个 Observable Acceptance Slice。
2. **RED**：先写一个 Focused Test。
3. 运行并确认失败原因确实是目标行为缺失/错误。Import Error、Broken Fixture、Environment Unavailable、Syntax Error 都不是有效 RED；先修复反馈回路。
4. **GREEN**：只写让当前 Test 通过所需的最小一致 Production Code，不提前实现未来 Slice。
5. 运行 Focused Test 和附近 Regression。
6. **REFACTOR**：只在 Green 状态改善命名/结构或去重复，不改变行为；再次运行 Tests。
7. 垂直重复，让每轮结果影响下一轮。

## 反模式
一次写完所有测试；用与 Production 相同算法计算 Expected Value；测试实现细节导致行为不变却因 Refactor 失败；过度 Mock 使真实 Consumer Path 从未执行；接受与目标行为无关的 Red Failure。

## 边界
TDD 是 Implementation Method，不是最终 Acceptance Proof。实现完成后使用 `evo-verify` 建立完整 Evidence Map。

## 输出
报告测试 Seam、RED 原因、GREEN 变更、实际运行 Tests，以及仍未覆盖的 Acceptance。
