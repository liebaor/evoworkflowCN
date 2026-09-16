# Harness compatibility

EVOworkflow 2.0 使用可移植 Agent Skill 正文和薄 Harness metadata。中文镜像保持与英文源相同的兼容性结构，仅翻译面向人的文字。

## Shared rules

- Skill directory 与 frontmatter `name` 使用相同 lowercase kebab-case ID。
- EVO-owned 核心指令不假设 slash command 或具体 `skill(...)` schema。
- Matt capability 以逻辑依赖名称引用。
- Supporting paths 在 Harness 暴露 Skill base directory 时使用相对路径。
- 中文翻译不得修改工具调用契约、路径或 ID。

## Installation shape

```sh
npx skills@latest add liebaor/evoworkflowCN
```

选择项目需要的 Matt Skills 与 EVO extensions。不要在同一目标再安装相同 Matt Skill ID。

## Codex

每个 EVO-owned Skill 包含 `agents/openai.yaml`。`display_name` 作为标题保持英文；说明可以中文化。需要用户控制生命周期的 Skill 使用：

```yaml
policy:
  allow_implicit_invocation: false
```

## OpenCode

EVO-owned Skill 使用：

```yaml
metadata:
  opencode/autoinvoke: "false"
```

从而保持显式调用，不让生命周期 Skill 随机自动触发。

## Claude Code

EVO-owned lifecycle Skill 保留：

```yaml
disable-model-invocation: true
```

其他 Harness 不认识某字段时应忽略它。

## Skill-to-Skill portability

跨 Harness 的安装/调用方式不同，因此正文使用 capability-based wording：

```text
apply `tdd`
apply `diagnosing-bugs`
```

而不是写死：

```text
/tdd
skill({id: "tdd"})
```

必需 Matt Skill 在当前 Harness/Session 无法加载时，返回 `MATT_SKILL_REQUIRED: <id>`，不要静默用另一套实现替代。

## Current target

优先对 Codex 与 OpenCode 做 combined Matt + EVO bundle 的行为测试；Claude Code 通过可移植 Skill 内容和 invocation frontmatter 保持兼容目标，并在可用 Runtime 中单独验证。
