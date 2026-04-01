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
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/runAgent.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/forkSubagent.ts`

## Main Points

- `getSystemPrompt()` returns default prompt parts, not the final prompt string.
- `SYSTEM_PROMPT_DYNAMIC_BOUNDARY` is conditional.
- interactive main-thread assembly in `REPL.tsx` differs from non-interactive assembly in `QueryEngine.ts`.
- ordinary subagents and fork subagents use different prompt inheritance models.
- startup and config choices keep affecting runtime behavior after launch.

## Conservative Boundaries

- keep `dynamic boundary` conditional in wording
- keep `mcp_instructions` narrow because it can move between inline sections and delta/attachment paths
- keep fork wording focused on preferential reuse rather than absolute equality
- keep `PROACTIVE`, `KAIROS`, and `COORDINATOR_MODE` as feature-gated branches, not fixed public modes

## Read Next

- [README.en.md](../README.en.md)
- [comparison.en.md](../comparison.en.md)
