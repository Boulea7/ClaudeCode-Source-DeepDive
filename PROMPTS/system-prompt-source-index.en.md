[简体中文](./system-prompt-source-index.md) | [English](./system-prompt-source-index.en.md)

# System Prompt Source Index

This page is an index and review aid. It does not dump the full raw system prompt.

## What This Page Does

- lists the main source files behind system prompt assembly
- separates the interactive, non-interactive, ordinary subagent, and fork subagent paths
- lists major sections, gates, and attachments that can reshape prompt behavior
- provides a verification checklist for future reviews

## Primary Source Files

- `_upstream/claude-code-sourcemap/restored-src/src/constants/prompts.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/constants/systemPromptSections.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/systemPrompt.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/queryContext.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/screens/REPL.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/QueryEngine.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/runAgent.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/forkSubagent.ts`

## Paths To Review

### 1. default prompt parts

- source:
  - `constants/prompts.ts -> getSystemPrompt()`
- check:
  - simple path
  - standard path
  - proactive / KAIROS path
  - whether `SYSTEM_PROMPT_DYNAMIC_BOUNDARY` is conditionally inserted

### 2. interactive main thread

- source:
  - `screens/REPL.tsx`
  - `utils/systemPrompt.ts -> buildEffectiveSystemPrompt()`
- check:
  - `getSystemPrompt()`
  - `getUserContext()`
  - `getSystemContext()`
  - `buildEffectiveSystemPrompt()`
  - `toolUseContext.renderedSystemPrompt`

### 3. non-interactive main thread

- source:
  - `utils/queryContext.ts`
  - `QueryEngine.ts`
- check:
  - `fetchSystemPromptParts()`
  - `customSystemPrompt`
  - `appendSystemPrompt`
  - `memoryMechanicsPrompt`
  - whether default prefetch is skipped when `customSystemPrompt` exists

### 4. ordinary subagent

- source:
  - `tools/AgentTool/runAgent.ts`
- check:
  - `agentDefinition.getSystemPrompt()`
  - `enhanceSystemPromptWithEnvDetails()`
  - `DEFAULT_AGENT_PROMPT` fallback

### 5. fork subagent

- source:
  - `tools/AgentTool/forkSubagent.ts`
  - `tools/AgentTool/runAgent.ts`
- check:
  - `renderedSystemPrompt`
  - exact tool set
  - `thinkingConfig`
  - `buildForkedMessages()`
  - gate conditions and fallback behavior

## Key Sections And Conditional Elements

- `SYSTEM_PROMPT_DYNAMIC_BOUNDARY`
- `mcp_instructions`
- `session_guidance`
- `output_style`
- `language`
- `memory`
- `env_info_simple`

## Review Checklist

- is `SYSTEM_PROMPT_DYNAMIC_BOUNDARY` described as conditional
- does `mcp_instructions` flow through inline sections or delta / attachments
- are interactive and non-interactive paths kept separate
- are ordinary subagents and fork subagents kept separate
- are `Buddy`, `KAIROS`, `PROACTIVE`, and `COORDINATOR_MODE` still described conservatively
- did any page accidentally paste large raw system prompt text

## Boundary Notes

- this page is a source index and does not dump large raw system prompt text
- feature gates show code branches, not rollout status
- the existence of a prompt path does not mean every build uses it
