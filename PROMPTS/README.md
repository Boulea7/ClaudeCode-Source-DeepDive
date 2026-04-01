# PROMPTS

这一部分只解释 **prompt 是怎么被组织、拼接和注入的**。

它更适合在你已经看过 [ARCHITECTURE.md](../ARCHITECTURE.md) 或至少知道 `main.tsx -> REPL.tsx / QueryEngine.ts -> query.ts` 这条主链之后再读。

不会做的事：

- 不复制大段原始 system prompt
- 不复制大段 tool prompt
- 不复制整份 skill body 或 agent body

会做的事：

- 说明 prompt 装配链
- 说明 section 的职责
- 先说明 REPL 与 headless / SDK 的 prompt 装配入口，再展开其它 prompt 影响面
- 给出关键源码路径
- 必要时指出哪些 prompt 路径仍受 feature gate 控制

## 建议阅读路线

### 第一步：先看主线程 prompt 怎么装

1. [system-prompt-assembly.md](./system-prompt-assembly.md)
2. [agent-prompts.md](./agent-prompts.md)

### 第二步：再看 section 和技能注入

3. [system-prompt-sections.md](./system-prompt-sections.md)
4. [skills-and-command-injection.md](./skills-and-command-injection.md)

### 第三步：最后看暴露面与风险

5. [exposure-surfaces-and-risks.md](./exposure-surfaces-and-risks.md)

## 这一组文档分别回答什么

- [system-prompt-assembly.md](./system-prompt-assembly.md)
  - default prompt parts、interactive 与 headless 的装配差异、fork 继承模型
- [system-prompt-sections.md](./system-prompt-sections.md)
  - section registry、dynamic boundary、哪些 section 会按运行时变化
- [agent-prompts.md](./agent-prompts.md)
  - 主线程、普通 subagent、fork subagent 三类 prompt 起点
- [skills-and-command-injection.md](./skills-and-command-injection.md)
  - `SKILL.md` 如何变成 `Command`、attachment 和模型可见上下文
- [exposure-surfaces-and-risks.md](./exposure-surfaces-and-risks.md)
  - prompt 暴露面、注入边界与高风险误写点

如果你想单独看 gate / 隐藏分支，请再读 [../FEATURE-FLAGS/README.md](../FEATURE-FLAGS/README.md)。
