[简体中文](./README.md) | [English](./README.en.md)

# Deep Dive: Prompts, Config, And Runtime Glue

This chapter groups prompt assembly, config influence, and startup/runtime glue that often spans other modules.

## What This Chapter Covers

- how default prompt parts are produced
- how section caching and conditional boundaries work
- how interactive and non-interactive main-thread prompt paths differ
- how ordinary subagents and fork subagents differ

## Key Source Files

- `_upstream/claude-code-sourcemap/restored-src/src/constants/prompts.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/constants/systemPromptSections.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/systemPrompt.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/queryContext.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/screens/REPL.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/QueryEngine.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/main.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/AgentTool.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/runAgent.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/forkSubagent.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/attachments.ts`

## Execution Flow

### 1. `getSystemPrompt()` returns default prompt parts

One boundary matters immediately: the default prompt and the final prompt are not the same thing.

`getSystemPrompt()` produces default prompt parts. In the standard path, those parts combine static sections and dynamic sections. `SYSTEM_PROMPT_DYNAMIC_BOUNDARY` appears only when the cache-scope conditions are met.

That is why the safer wording is “default prompt parts factory” rather than “the one final system prompt string”.

### 2. Section caching is its own layer

`systemPromptSections.ts` is not just content. It manages section-level caching behavior:

- which sections can be cached
- which sections must be recomputed
- how cache invalidation works after commands such as `/clear` or compaction-related resets

This is also where prompt fragments such as `mcp_instructions` need careful wording, because their final presentation can depend on runtime path and attachment-backed behavior.

### 3. The interactive main thread assembles the final prompt in `REPL.tsx`

The interactive path does not go through `QueryEngine.ts` first.

Instead, `REPL.tsx` reads current tools and MCP state, assembles the effective prompt, and then enters `query()`. That path is the reason interactive prompt precedence should stay distinct from headless or SDK wording.

The current mirror supports a more specific rule here:

- interactive prompt assembly is a REPL-side runtime concern
- prompt choice and tool-pool state are shaped together before `query()`

### 4. The non-interactive path uses a different precedence chain

`QueryEngine.ts` does not simply reuse the interactive precedence helper.

The non-interactive path combines:

- `customSystemPrompt ?? defaultSystemPrompt`
- optional memory-mechanics additions in a narrower branch
- `appendSystemPrompt`

`queryContext.ts` also shows that when a custom system prompt exists, the default prompt factory and some default context prefetch steps can be skipped.

That is why interactive and non-interactive prompt assembly should stay documented as different runtime chains.

### 5. Ordinary subagents and fork subagents use different inheritance models

The current mirror supports a clear split:

- ordinary subagents start from `agentDefinition.getSystemPrompt()` and then go through environment-detail enhancement
- fork subagents preferentially reuse the parent’s rendered prompt, tool set, and message-prefix reconstruction path

The conservative wording still matters here:

- fork prefers reuse
- fork does not prove byte-for-byte absolute equality with the parent prompt path in every fallback branch

### 6. Startup and config decisions keep shaping later turns

This chapter also matters because it ties startup-time choices to later runtime behavior.

Prompt-related config, feature-gated branches, and mode-specific switches keep influencing:

- the prompt parts that exist
- the prompt sections that remain dynamic
- which main-thread path is active
- how agent prompts are added or appended

That is why this module belongs with runtime glue, not with prompt text alone.

## Why This Layer Matters

Prompt assembly in Claude Code is not a single string template. The current mirror shows a runtime structure with:

- named prompt parts
- named dynamic sections
- cache behavior
- separate main-thread precedence chains
- separate subagent inheritance models

That structure directly affects prompt reuse, cache sharing, agent inheritance, and how feature-gated branches such as `PROACTIVE`, `KAIROS`, or coordinator-related paths appear.

## Conservative Boundaries

- keep `SYSTEM_PROMPT_DYNAMIC_BOUNDARY` described as conditional
- keep `mcp_instructions` narrow because it can move between inline sections and attachment-backed delta paths
- keep fork wording focused on preferential reuse rather than absolute equality
- keep `PROACTIVE`, `KAIROS`, and `COORDINATOR_MODE` as feature-gated branches, not fixed public modes
- keep startup and config wording limited to client-side source evidence

## Read Next

- [README.en.md](../README.en.md)
- [comparison.en.md](../comparison.en.md)
