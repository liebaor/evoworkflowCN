---
name: evo-spec
description: 把已经理解并达成一致的非简单 Intent 综合成 `.evo/specs/` 下的 Working Spec。行为、Contract、架构、长期格式或跨 Session 工作需要明确 Acceptance Owner 时使用；不要在这里继续采访未解决的产品决策。
---

# EVO Spec

## Preconditions
重大产品/架构选择已经确定；否则回到 `evo-grill-with-docs`。需要最新外部研究的事实也已解决。

## Read first
`.evo/project.md`、`.evo/context.md`、相关 Decisions/Research、当前 Source/Contracts/Tests，以及已确定的用户 Outcome。

## Workflow
创建/更新一个 `.evo/specs/<change>.md`，包含：Solution-independent Problem、Desired Outcome、Non-goals、当前相关行为/Pattern、Proposed Direction、真实 Alternatives 及其劣势、Risks/Trade-offs、Observable Acceptance；每条 Acceptance 对应 Likely Failure Surface 和 Direct Evidence Path；剩余非阻塞 Unknown。

不要为了文档变长而加入脆弱的实现细节。

## Lifecycle
Working Spec 描述 Intended Change，不是 Current Truth。实现/Review 后，`evo-finish` 把长期 Rationale 收敛到 Decisions/Current Docs，并避免过时 Proposal 被误认为当前行为。

## Output
返回 Spec 路径、关键 Acceptance，并默认推荐 `evo-plan`；足够小的 Change 可直接进入实现。
