# Codex Prompt Engineering

一个面向 Codex、Cline 和其他 AI 编码代理的工程任务整理 skill。用于生成可直接交接的 Prompt，保留关键事实、范围和验收条件。

## 目标

将需求、讨论、Bug 报告、重构想法或架构方案整理成工程 Prompt，减少歧义和无效上下文。事实未明时，输出明确的发现任务和实施边界。

这是指令型 skill，没有额外执行工具。实际收益需要通过真实任务对照验证；不承诺编码成功率、Token 或总耗时改善。

## 适用场景

- 把自然语言需求转换为 Codex/Cline 任务 Prompt。
- 编写实现规格、工程蓝图或验证计划。
- 压缩长讨论，同时保留关键决策和约束。
- 将 Bug 报告整理为包含复现、根因验证和回归测试的修复 Prompt。
- 将重构、代码审查或架构设计要求整理成代理可执行任务。

普通代码实现、调试、安全审查、测试、UI 设计、调研和文档任务不应自动触发本 skill；这些任务仍应使用对应的专门 skill。

## 按任务选择篇幅

| 形式 | 适用情况 | 输出重点 |
| --- | --- | --- |
| 短指令 | 范围明确、风险低的小修改 | 目标、限制、适量验证；无需固定章节 |
| 结构化任务书 | 多行为、接口或验收约束需要协调 | 当前决定、范围、契约、实施要求和验收 |
| 发现任务书 | 根因、目标或关键契约尚未确定 | 检查什么、如何取得证据、哪些工作依赖结论 |

已有完整规格时，优先提取当前任务或定向修改，避免重复重写。三个虚构示例见 [references/examples.md](references/examples.md)，仅在需要参考写法时读取。

## 结构化 Prompt 的可选章节

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

## 关键行为

- 区分用户要求、已核实事实、转述或待验证假设、可选建议。关键事实保留来源和适用范围。
- 整理长讨论时识别最新明确修订、已撤销决定和未解决冲突；后续局部修改不取消其他边界。
- 不把疑似根因改写成指定修复方案，也不把生成 Prompt 的授权扩展为实施授权。
- 验收命令从已提供信息或实际仓库中取得；未知时要求先发现，不假设工具和环境可用。
- 区分计划验证、已有证据和未验证事项；源码或构建成功不能替代明确要求的运行时或人工验收。
- 输出前对照原始要求检查遗漏和新增要求；默认不额外输出检查表。

行为细则以 [SKILL.md](SKILL.md) 为准。抽查素材与验证记录见 [evals/README.md](evals/README.md)；提示词行为抽查不等于实际编码效果评测。

## 使用

在 Codex 中显式调用：

```text
Use $codex-prompt-engineering to turn this requirement into an implementation-ready prompt:
...
```

可按需在个人或项目的 `AGENTS.md` 中配置调用规则；无需把整份 skill 重复写入。保留已有的自动发现策略，普通工程任务仍交给对应工作流。

## License

建议发布前根据你的 GitHub 仓库策略补充许可证。当前 skill 本身未声明独立许可证。
