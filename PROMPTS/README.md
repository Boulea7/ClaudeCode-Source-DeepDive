[简体中文](./README.md) | [English](./README.en.md)

# PROMPTS

这一组文档记录 Claude Code 在当前镜像里的 prompt 装配机制、注入入口、源码锚点与复核边界。

## 阅读顺序

1. [system-prompt-assembly.md](./system-prompt-assembly.md)
2. [system-prompt-sections.md](./system-prompt-sections.md)
3. [agent-prompts.md](./agent-prompts.md)
4. [skills-and-command-injection.md](./skills-and-command-injection.md)
5. [exposure-surfaces-and-risks.md](./exposure-surfaces-and-risks.md)
6. [system-prompt-source-index.md](./system-prompt-source-index.md)

## 术语卡片

- `gate`
  - 编译期或运行时分支开关。源码里出现 gate 代表存在分支，不代表该分支已经对外开放。
- `rollout`
  - 某条 gated path 在某个构建、账号、订阅层级或实验组里实际打开的发布状态。静态源码不能单独证明 rollout。
- `attachment-backed delta path`
  - 变化量不直接内联进主 system prompt section，运行时改用 attachment 注入增量。当前本轮可确认的例子是 `mcp_instructions_delta`，入口在 `attachments.ts`。
- `ordinary subagent`
  - 显式提供 `subagent_type` 的普通子代理路径。它使用 agent 自己的 prompt 起点，再做 env/details 增强。
- `fork subagent`
  - `FORK_SUBAGENT` 开启且省略 `subagent_type` 时触发的隐式 fork 路径。它优先复用父线程 `renderedSystemPrompt` 与消息前缀。
- `dynamic boundary`
  - `SYSTEM_PROMPT_DYNAMIC_BOUNDARY`。它把可跨会话缓存的静态前缀和按会话变化的动态段落分开。该标记按条件插入。

## 本组文档的写法边界

- 只讲装配机制、注入入口、可见面与保守边界。
- 不转储大段 raw system prompt 或 raw agent prompt。
- 不把 feature gate 写成 rollout 结论。
- 不把 fork、ordinary subagent、interactive main thread、non-interactive main thread 混写成同一条链。

## 本轮直接回读的主干源码

- `_upstream/claude-code-sourcemap/restored-src/src/constants/prompts.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/constants/systemPromptSections.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/systemPrompt.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/queryContext.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/screens/REPL.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/QueryEngine.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/AgentTool.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/runAgent.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/forkSubagent.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/attachments.ts`
