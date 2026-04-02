[简体中文](./agent-prompts.md) | [English](./agent-prompts.en.md)

# Agent Prompt Sources

This page separates main-thread and subagent prompt sources. It stays on assembly mechanics and does not dump raw prompt text.

## Key Source Files

- `_upstream/claude-code-sourcemap/restored-src/src/utils/systemPrompt.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/queryContext.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/screens/REPL.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/QueryEngine.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/AgentTool.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/runAgent.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/forkSubagent.ts`

## Confirmed From Source

- The interactive main thread in `REPL.tsx` fetches `getSystemPrompt()`, `getUserContext()`, and `getSystemContext()`, then calls `buildEffectiveSystemPrompt()`, then stores the rendered result in `toolUseContext.renderedSystemPrompt`.
- `buildEffectiveSystemPrompt()` applies this priority:
  - `overrideSystemPrompt`
  - coordinator prompt, only when `COORDINATOR_MODE` is active, the env flag is truthy, and no `mainThreadAgentDefinition` is present
  - `mainThreadAgentDefinition` prompt
  - `customSystemPrompt`
  - `defaultSystemPrompt`
- Built-in main-thread agents call `getSystemPrompt({ toolUseContext })`. Non-built-in agents call a no-argument `getSystemPrompt()`.
- When `PROACTIVE` or `KAIROS` is active and the proactive runtime is active, main-thread agent instructions are appended after the default prompt as `# Custom Agent Instructions`.
- The non-interactive main thread uses `queryContext.ts -> fetchSystemPromptParts()` plus `QueryEngine.ts` and `asSystemPrompt([...])`.
- When `customSystemPrompt` is present, `fetchSystemPromptParts()` skips the default `getSystemPrompt()` and `getSystemContext()` prefetch.
- In `QueryEngine.ts`, `customSystemPrompt` plus `hasAutoMemPathOverride()` adds `memoryMechanicsPrompt`.
- Ordinary subagents use `runAgent.ts:getAgentSystemPrompt()`, which calls `agentDefinition.getSystemPrompt(...)`, then `enhanceSystemPromptWithEnvDetails(...)`, with `DEFAULT_AGENT_PROMPT` as fallback.
- `AgentTool.tsx` routes to the fork path when `subagent_type` is omitted and the fork gate is enabled.
- The fork path prefers the parent `toolUseContext.renderedSystemPrompt`. If it is missing, the code recomputes it and explicitly warns that the fallback may drift.
- `forkSubagent.ts:buildForkedMessages()` clones the parent assistant message, preserves all `tool_use` blocks, synthesizes placeholder `tool_result` blocks, and appends a child directive.

## Not Confirmed From Source

- Rollout state for `COORDINATOR_MODE`, `PROACTIVE`, `KAIROS`, and `FORK_SUBAGENT`.
- The exact final prompt bytes in a live runtime, because dynamic sections, memory, attachments, and GrowthBook state still reshape the result.
- The real-world divergence range between fork fallback recomputation and the parent `renderedSystemPrompt`.

## Review Checklist

- Keep interactive and non-interactive paths separate.
- Keep ordinary subagents and fork subagents separate.
- Keep `renderedSystemPrompt` described as a fork-stability anchor.
- Preserve the conditional coordinator branch in `buildEffectiveSystemPrompt()`.
- Do not paste large raw agent prompt bodies into the docs.
