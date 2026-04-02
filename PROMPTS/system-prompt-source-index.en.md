[简体中文](./system-prompt-source-index.md) | [English](./system-prompt-source-index.en.md)

# System Prompt Source Index

This page is a source index and review map. It does not dump raw prompts.

## Main Index

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
  - the `toolUseContext.renderedSystemPrompt` writeback points
- `_upstream/claude-code-sourcemap/restored-src/src/QueryEngine.ts`
  - non-interactive main-thread prompt assembly
  - `memoryMechanicsPrompt`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/AgentTool.tsx`
  - fork routing when `subagent_type` is omitted
  - preferred reuse of the parent `renderedSystemPrompt`
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

## What The Current Source Confirms

- The static prefix, dynamic boundary, section registry, interactive assembly path, headless assembly path, ordinary subagent path, fork subagent path, and attachment injection entry points all have direct source anchors.
- `AgentTool.tsx` plus `forkSubagent.ts` define the split between ordinary subagents and fork subagents.
- `attachments.ts` is the main prompt-adjacent delta surface. `mcp_instructions_delta`, `skill_listing`, and `task_status` are generated there and wrapped into attachment messages.

## What The Current Source Does Not Confirm

- Rollout for any gate.
- The full raw prompt for any live session.
- Any server-side experiment allocation.

## Review Checklist

- For main-thread prompt behavior, start from `prompts.ts`, `systemPrompt.ts`, `REPL.tsx`, and `QueryEngine.ts`.
- For subagent prompt behavior, start from `AgentTool.tsx`, `runAgent.ts`, and `forkSubagent.ts`.
- For prompt-adjacent delta surfaces, start from `attachments.ts` and `processPromptSlashCommand.tsx`.
- Do not copy large raw prompt blocks into the docs.
