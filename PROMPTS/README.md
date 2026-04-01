[简体中文](./README.md) | [English](./README.en.md)

# PROMPTS

这一组文档解释 Claude Code 的 prompt 装配与注入机制。

这里重点回答四类问题：

- default prompt parts 从哪里来
- interactive 与 non-interactive 主线程怎样组装 system prompt
- ordinary subagent 与 fork subagent 在 prompt 来源上有什么差异
- skills、attachments、gates 怎样影响模型可见上下文

## 建议阅读顺序

1. [system-prompt-assembly.md](./system-prompt-assembly.md)
2. [agent-prompts.md](./agent-prompts.md)
3. [system-prompt-sections.md](./system-prompt-sections.md)
4. [skills-and-command-injection.md](./skills-and-command-injection.md)
5. [system-prompt-source-index.md](./system-prompt-source-index.md)
6. [exposure-surfaces-and-risks.md](./exposure-surfaces-and-risks.md)

## 术语说明

- `default prompt parts`
  - `getSystemPrompt()` 返回的一组 prompt 片段
- `interactive main thread`
  - `main.tsx -> REPL.tsx -> query.ts`
- `non-interactive main thread`
  - `main.tsx -> QueryEngine.ts -> query.ts`
- `ordinary subagent`
  - 使用 agent 自己的 prompt 起点
- `fork subagent`
  - 优先复用父线程已经渲染的 prompt 与消息前缀
- `dynamic boundary`
  - 条件插入的 `SYSTEM_PROMPT_DYNAMIC_BOUNDARY`

## 这组文档不做什么

- 不贴大段 raw prompt
- 不把 feature-gated 分支写成公开发布结论
- 不把 prompt 装配说明写成唯一固定流程
