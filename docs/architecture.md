# EVOworkflow 架构

## 定位

EVOworkflow 是一套由 Skill 驱动、采用固定 Repository 知识约定的软件工程方法。

它明确区分四种权威：

- **Human Authority**：产品方向、重大取舍与授权。
- **Semantic Authority**：Agent 基于 Repository 证据进行语义推理。
- **Deterministic Authority**：项目原生 tests/build/lint/runtime/CI。
- **Historical Authority**：Git 时间线与交付历史。

## 固定知识工作区

所有采用 EVO 的 Repository 都使用 `.evo/`：

```text
.evo/
├── project.md
├── context.md
├── goal.md
├── decisions/
├── specs/
├── plans/
└── research/
```

它是工程知识工作区，不是运行时数据库。文件保持人类可读的 Markdown；不需要隐藏的 workflow state、phase lock、fingerprint 或通用 gate。

### 各目录职责

- `project.md`：项目地图和运行导航。
- `context.md`：领域语言与稳定业务事实。
- `decisions/`：长期设计理由和可复盘工程决策。
- `specs/`：尚未完成的目标行为/设计。
- `plans/`：可执行 Slice 拆分。
- `research/`：带日期的外部证据及对项目的影响。
- `goal.md`：当前或最近一次长时间执行目标记录。

正式产品/项目文档仍放在项目原本的位置；`.evo/` 不替代 API 手册、部署指南或用户文档。

## Convention over discovery

知识位置必须是确定的。Brownfield 接入时，把属于 EVO 的工程知识迁移进 `.evo/` 并更新引用，而不是让未来每个 Agent 学一套项目特有映射。

知识内容仍需要语义判断：Agent 必须读取源码、测试、文档、Git 与运行证据，才能判断事实。

## 编排边界

`evo-goal` 只负责一个 Repository、一个 Active Goal、一个 Writer 的 Skill 级循环。它不是多 Agent 调度平台，也不实现运行时。更大的编排属于 Harness。

## 验证边界

EVO 定义 Evidence discipline；宿主项目工具负责产生证据。Build 绿色只证明可构建；Unit Test 只证明对应 seam 的行为；Browser/runtime 检查只证明实际执行到的路径；无法获得证据的边界必须保留为 UNVERIFIED。

## 交付边界

`evo-finish` 负责让 Current Truth 收敛，`evo-commit` 负责记录交付历史。Commit 与 Push 都不能替代 Verify 或 Review。
