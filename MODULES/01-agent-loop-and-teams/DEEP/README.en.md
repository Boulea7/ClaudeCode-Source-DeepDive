[简体中文](./README.md) | [English](./README.en.md)

# Deep Dive: Agent Loop And Teams

This chapter explains how the main thread, child agents, task state, and team-oriented execution fit into one runtime chain.

## What This Chapter Covers

- the interactive and non-interactive entry paths
- where `AgentTool` fits in the orchestration chain
- how `runAgent()` differs from `AgentTool`
- how local agents, remote agents, shell tasks, and teammates share task-state layers

## Key Source Files

- `_upstream/claude-code-sourcemap/restored-src/src/main.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/screens/REPL.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/QueryEngine.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/query.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/AgentTool.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/runAgent.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/forkSubagent.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tasks/`

## Main Points

- Interactive main-thread execution primarily follows `main.tsx -> REPL.tsx -> query.ts`.
- Non-interactive / SDK execution primarily follows `main.tsx -> QueryEngine.ts -> query.ts`.
- `AgentTool` chooses the child-agent path and launch mode.
- `runAgent()` executes the child session on the same underlying runtime.
- fork subagents and ordinary subagents use different inheritance models.
- `tasks/` is a runtime state layer, not just a display layer.

## Conservative Boundaries

- `requiredMcpServers` checks are visible in runtime code, but broader authoring guarantees for custom agents still need conservative wording.
- foreground-to-background transitions should be described as task identity continuity, not as one unchanged execution instance magically switching threads.
- some task variants are declared in types but not fully represented in the current readable mirror.

## Read Next

- [README.en.md](../README.en.md)
- [comparison.en.md](../comparison.en.md)
