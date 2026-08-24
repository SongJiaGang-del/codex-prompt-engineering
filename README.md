# Codex Prompt Engineering

一个面向 Codex、Cline 和其他 AI 编码代理的高质量 Prompt skill。

## 目标

将需求、讨论、Bug 报告、重构想法或架构方案整理成可直接执行的工程 Prompt，减少歧义和无效上下文，同时保留实现所需的关键事实。

该 skill 优先保证：

1. 正确性
2. 安全性
3. 兼容性
4. 可验证性
5. Token 效率

## 适用场景

- 把自然语言需求转换为 Codex/Cline 任务 Prompt。
- 编写实现规格、工程蓝图或验证计划。
- 压缩长讨论，同时保留关键决策和约束。
- 将 Bug 报告整理为包含复现、根因验证和回归测试的修复 Prompt。
- 将重构、代码审查或架构设计要求整理成代理可执行任务。

普通代码实现、调试、安全审查、测试、UI 设计、调研和文档任务不应自动触发本 skill；这些任务仍应使用对应的专门 skill。

## Prompt 结构

根据任务选择必要章节：

```text
[Context]
[Objective]
[Scope]
[Files and Interfaces]
[Constraints]
[Implementation Requirements]
[Verification]
[Deliverables]
[Assumptions and Questions]
```

空章节应省略。未知的文件、API、依赖、测试结果或产品行为不得编造，应要求代理先检查仓库。

## 设计原则

- 用可观察行为替代“正确处理”“优化一下”等模糊表述。
- 明确必做项、建议项和非目标。
- 同时描述正常流程和失败行为。
- 使用已知的精确文件名、类型、路由、接口和函数签名。
- 每条验收标准都应可以独立检查。
- 区分源代码、构建、测试和浏览器运行时证据。
- 提示词应足够简洁，但不得为了省 Token 删除影响实现决策的上下文。

## 使用

在 Codex 中显式调用：

```text
Use $codex-prompt-engineering to turn this requirement into an implementation-ready prompt:
...
```

核心规则位于 [SKILL.md](SKILL.md)。Codex 的个性化自动调用规则位于 `C:\Users\35741\.codex\AGENTS.md`。

## License

建议发布前根据你的 GitHub 仓库策略补充许可证。当前 skill 本身未声明独立许可证。
