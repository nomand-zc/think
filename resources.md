# 资料
## Prompt caching
基于prompt cache能力，提升相同前缀内容的处理速度，节省token。

- [Openai promt cache介绍](https://platform.openai.com/docs/guides/prompt-caching)
- [anthropic promt cache介绍](https://platform.claude.com/docs/zh-CN/build-with-claude/prompt-caching)

## 上下文工程管理
- [设计方案](https://github.com/nomand-zc/think/blob/main/agent%E5%8E%86%E5%8F%B2%E5%AF%B9%E8%AF%9D%E7%AE%A1%E7%90%86%E6%96%B9%E6%A1%88%E8%AE%BE%E8%AE%A1.md)
- [deepagents](https://github.com/langchain-ai/deepagents)
- 方案：
  - 压缩：当对话接近上下文窗口限制时，总结核心内容（保留架构决策、未解决问题等），丢弃冗余信息（如工具原始输出），用摘要重新启动新上下文窗口
  - 即时上下文检索: 维护轻量级标识符（文件路径、查询、链接等），运行时通过工具动态加载数据，不预先处理全部数据（类似人类按需检索信息）
  - 混合检索策略: 结合 “预先加载关键数据” 和 “运行时自主探索”，平衡速度与上下文完整性
  - 内容裁剪: 将带有大文本工具的内容卸载（如read工具结果、write工具的参数）。
  - 动态上下文发现: 仅保留高频使用的原子工具以及工具发现工具，将低频工具卸载，通过发现工具按需动态加载 [文档](https://cursor.com/cn/blog/dynamic-context-discovery)
  - 使用程序化调用执行替代step by step的工具调用。[高级工具使用](https://www.anthropic.com/engineering/advanced-tool-use)
  - 使用工具示例来弥补JSON Schema无法表达的使用模式。例如：date参数在JSON Schema中只能指定string类型，不能进一步表达date字段的类型为“2024-11-06”、“2024年11月6日”还是“2024-11-06T00:00:00Z”？
  - 子代理模式：通过子代理，隔离上下文信息。缩减单个代理上下文占用大小。核心在于如何贡献信息：
    - 接收独立子任务，不共享父代理上下文，仅返回子代理的任务结果（类似agentTool）
    - 共享父代理的上下文，仅让子代理的任务结论对父代理可见
    - 多个子代理之间不共享信息

## 技能仓库
- [本地化](https://github.com/ComposioHQ/awesome-claude-skills/blob/master/raffle-winner-picker/SKILL.md)
- [anthropic](https://github.com/anthropics/skills)

## coding agent
- [crush](https://github.com/charmbracelet/crush)
- [opencode](https://github.com/anomalyco/opencode)

## RAG 优化技术
- 引入上下文检索: 核心思路， 将完整文档与当前块内容输入给LLM，生成一个50-80字以内的上下文信息编入当前块中[文档](https://www.anthropic.com/engineering/contextual-retrieval)
- 推荐：
  - Embeddings+BM25 比单独使用嵌入更好
  - 根据场景选择合适的embedding模型（关注：领域、语言、语义复杂度（与维度有关）、token限制以及最佳token大小）
  - 将前 20 个数据块传递给模型比只传递前 10 个或前 5 个数据块更有效
  - 为数据块添加上下文信息可以大大提高检索准确率
  - 重新排名总比不重新排名好

## Agent效果评估
  - [参考文章](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)