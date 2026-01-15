# 资料
## Prompt caching
基于prompt cache能力，提升相同前缀内容的处理速度，节省token。

- [Openai](https://platform.openai.com/docs/guides/prompt-caching)
- [anthropic](https://platform.claude.com/docs/zh-CN/build-with-claude/prompt-caching)

## 上下文工程管理
- [设计方案](https://github.com/nomand-zc/think)
- [deepagents](https://github.com/langchain-ai/deepagents)
- 优化：
 - 内容裁剪: 将带有大文本工具的内容卸载（如read工具结果、write工具的参数）。
 - 工具上下文缩减: 仅保留高频使用的原子工具以及工具发现工具，将低频工具卸载，通过发现工具按需动态加载
 - 使用程序化调用执行替代step by step的工具调用。[高级工具使用](https://www.anthropic.com/engineering/advanced-tool-use)
 - 使用工具示例来弥补JSON Schema无法表达的使用模式。例如：date参数在JSON Schema中只能指定string类型，不能进一步表达date字段的类型为“2024-11-06”、“2024年11月6日”还是“2024-11-06T00:00:00Z”？

## 技能仓库
- [本地化](https://github.com/ComposioHQ/awesome-claude-skills/blob/master/raffle-winner-picker/SKILL.md)
- [anthropic](https://github.com/anthropics/skills)

## coding agent
- [crush](https://github.com/charmbracelet/crush)
- [opencode](https://github.com/anomalyco/opencode)