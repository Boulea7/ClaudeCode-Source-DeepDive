[简体中文](./system-prompt-source-index.md) | [English](./system-prompt-source-index.en.md)

# System Prompt Source Index

这一页提供源码索引和复核锚点，不转储 raw prompt。

## 主索引

- `_upstream/claude-code-sourcemap/restored-src/src/constants/prompts.ts`
  - `getSystemPrompt()`
  - `SYSTEM_PROMPT_DYNAMIC_BOUNDARY`
  - `getSessionSpecificGuidanceSection()`
- `_upstream/claude-code-sourcemap/restored-src/src/constants/systemPromptSections.ts`
  - `systemPromptSection()`
  - `DANGEROUS_uncachedSystemPromptSection()`
  - `resolveSystemPromptSections()`
  - `clearSystemPromptSections()`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/systemPrompt.ts`
  - `buildEffectiveSystemPrompt()`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/queryContext.ts`
  - `fetchSystemPromptParts()`
  - `buildSideQuestionFallbackParams()`
- `_upstream/claude-code-sourcemap/restored-src/src/screens/REPL.tsx`
  - interactive main-thread prompt assembly
  - `toolUseContext.renderedSystemPrompt` 写回点
- `_upstream/claude-code-sourcemap/restored-src/src/QueryEngine.ts`
  - non-interactive main-thread prompt assembly
  - `memoryMechanicsPrompt`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/AgentTool.tsx`
  - `subagent_type` 缺失时的 fork 路由
  - fork path 对父 `renderedSystemPrompt` 的优先复用
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/runAgent.ts`
  - `getAgentSystemPrompt()`
  - `DEFAULT_AGENT_PROMPT` fallback
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/forkSubagent.ts`
  - `isForkSubagentEnabled()`
  - `buildForkedMessages()`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/attachments.ts`
  - `getMcpInstructionsDeltaAttachment()`
  - `getSkillListingAttachments()`
  - `getUnifiedTaskAttachments()`
  - `createAttachmentMessage()`

## 当前源码能确认什么

- system prompt 的静态前缀、动态 boundary、section registry、interactive 装配、headless 装配、ordinary subagent、fork subagent、attachment 注入入口都能定位到直接源码锚点。
- `AgentTool.tsx` 与 `forkSubagent.ts` 共同定义了 ordinary subagent 与 fork subagent 的分叉点。
- `attachments.ts` 是 prompt 外增量可见面的核心入口。`mcp_instructions_delta`、`skill_listing`、`task_status` 都在这里生成并被包成 attachment message。

## 当前源码不能确认什么

- 任何 gate 的 rollout。
- 任何真实会话里的完整 raw prompt。
- 任何服务端侧实验分桶。

## 复核清单

- 需要解释 main-thread prompt 时，优先从 `prompts.ts`、`systemPrompt.ts`、`REPL.tsx`、`QueryEngine.ts` 开始。
- 需要解释 subagent prompt 时，优先从 `AgentTool.tsx`、`runAgent.ts`、`forkSubagent.ts` 开始。
- 需要解释增量可见面时，优先从 `attachments.ts` 与 `processPromptSlashCommand.tsx` 开始。
- 文档里不复制大段 raw prompt。
