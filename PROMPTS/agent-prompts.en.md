[简体中文](./agent-prompts.md) | [English](./agent-prompts.en.md)

# Main Thread And Agent Prompt Sources

This page separates the prompt origins for the interactive main thread, the non-interactive main thread, ordinary subagents, and fork subagents.

## What This Page Explains

- where the interactive main-thread prompt comes from
- why the non-interactive main-thread path is different
- what ordinary subagents use as their prompt origin
- why fork subagents reuse `renderedSystemPrompt`

## Main Points

- interactive main-thread prompt assembly happens in `REPL.tsx`
- non-interactive prompt assembly happens through `QueryEngine.ts` and `queryContext.ts`
- ordinary subagents use `agentDefinition.getSystemPrompt()` and then `enhanceSystemPromptWithEnvDetails()`
- fork subagents preferentially reuse the parent prompt and rebuild a cache-friendly prefix

## Conservative Boundaries

- `COORDINATOR_MODE`, `PROACTIVE`, `KAIROS`, and `FORK_SUBAGENT` remain feature-gated paths
- fork behavior should stay described as preferential reuse, not absolute identity
- final runtime prompt bytes still depend on active context, memory, and gate state
