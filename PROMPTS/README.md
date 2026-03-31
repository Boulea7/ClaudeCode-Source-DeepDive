# PROMPTS

这一部分只解释 **prompt 是怎么被组织、拼接和注入的**。

不会做的事：

- 不复制大段原始 system prompt
- 不复制大段 tool prompt
- 不复制整份 skill body 或 agent body

会做的事：

- 说明 prompt 装配链
- 说明 section 的职责
- 先说明 REPL 与 headless / SDK 的 prompt 装配入口，再展开其它 prompt 影响面
- 给出关键源码路径

建议阅读顺序：

1. [system-prompt-assembly.md](./system-prompt-assembly.md)
2. [system-prompt-sections.md](./system-prompt-sections.md)
3. [agent-prompts.md](./agent-prompts.md)
4. [skills-and-command-injection.md](./skills-and-command-injection.md)
5. [exposure-surfaces-and-risks.md](./exposure-surfaces-and-risks.md)
