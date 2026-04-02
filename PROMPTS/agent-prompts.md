[简体中文](./agent-prompts.md) | [English](./agent-prompts.en.md)

# Agent Prompts

这一页拆开主线程与子代理的 prompt 来源。它只讲装配来源，不转储原始 prompt 文本。

## 关键源码文件

- `_upstream/claude-code-sourcemap/restored-src/src/utils/systemPrompt.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/queryContext.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/screens/REPL.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/QueryEngine.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/AgentTool.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/runAgent.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/forkSubagent.ts`

## 当前源码能确认的机制

- interactive main thread 在 `REPL.tsx` 里先拉 `getSystemPrompt()`、`getUserContext()`、`getSystemContext()`，再调用 `buildEffectiveSystemPrompt()`，随后把结果写回 `toolUseContext.renderedSystemPrompt`。
- `buildEffectiveSystemPrompt()` 的优先级是：
  - `overrideSystemPrompt`
  - coordinator prompt。条件是 `COORDINATOR_MODE` 打开、环境变量为真、当前没有 `mainThreadAgentDefinition`
  - `mainThreadAgentDefinition` 的 prompt
  - `customSystemPrompt`
  - `defaultSystemPrompt`
- built-in main-thread agent 通过 `getSystemPrompt({ toolUseContext })` 取 prompt。非 built-in agent 走无参 `getSystemPrompt()`。
- `PROACTIVE` 或 `KAIROS` 激活且 proactive runtime 处于活动状态时，main-thread agent prompt 会以 `# Custom Agent Instructions` 的形式追加在 `defaultSystemPrompt` 后面。
- non-interactive main thread 走 `queryContext.ts -> fetchSystemPromptParts()` 与 `QueryEngine.ts` 的 `asSystemPrompt([...])` 组合链。
- `customSystemPrompt` 存在时，`fetchSystemPromptParts()` 会跳过默认 `getSystemPrompt()` 和 `getSystemContext()` 预取。
- `QueryEngine.ts` 在 `customSystemPrompt` 存在且 `hasAutoMemPathOverride()` 为真时，会额外注入 `memoryMechanicsPrompt`。
- ordinary subagent 走 `runAgent.ts:getAgentSystemPrompt()`。这条链会调用 `agentDefinition.getSystemPrompt(...)`，再进入 `enhanceSystemPromptWithEnvDetails(...)`，失败时退回 `DEFAULT_AGENT_PROMPT`。
- fork subagent 由 `AgentTool.tsx` 决定路由。省略 `subagent_type` 且 fork gate 打开时，`effectiveType` 保持 `undefined`，随后进入 fork path。
- fork path 优先复用父线程 `toolUseContext.renderedSystemPrompt`。缺失时会回退到重新计算，源码注释明确写明该回退可能发生 drift。
- `forkSubagent.ts:buildForkedMessages()` 会克隆父 assistant message，保留全部 `tool_use` block，合成占位 `tool_result`，再附上 child directive。

## 当前源码不能确认的内容

- `COORDINATOR_MODE`、`PROACTIVE`、`KAIROS`、`FORK_SUBAGENT` 在公开构建里的 rollout 状态。
- 某个运行时里的最终 prompt 字节内容。动态 sections、memory、attachments、GrowthBook 状态都会继续改写结果。
- fork 回退重算与父线程 `renderedSystemPrompt` 的实际偏差范围。

## 复核清单

- interactive 与 non-interactive 是否被分成两条链。
- ordinary subagent 与 fork subagent 是否被分开描述。
- `renderedSystemPrompt` 是否被写成 fork 稳定性锚点。
- `buildEffectiveSystemPrompt()` 的优先级是否保留 coordinator 条件。
- 文档里是否出现大段 raw agent prompt。
