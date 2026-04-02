[简体中文](./agent-memory-compact-gates.md) | [English](./agent-memory-compact-gates.en.md)

# Agent, Memory, And Compact Gates

This page tracks the gates around agents, memory paths, compaction paths, and task-layer switching.

## Key Source Files

- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/AgentTool.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/runAgent.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/forkSubagent.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/services/SessionMemory/sessionMemory.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/memdir/memdir.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/memdir/paths.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/memdir/teamMemPaths.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/services/compact/autoCompact.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/query.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/tasks.ts`

## Confirmed From Source

- `FORK_SUBAGENT` sends Agent calls with omitted `subagent_type` into the fork path.
- When `FORK_SUBAGENT` is active, the `AgentTool` schema hides `run_in_background`.
- `CLAUDE_CODE_DISABLE_BACKGROUND_TASKS` disables background-task behavior globally.
- `CLAUDE_AUTO_BACKGROUND_TASKS` or `tengu_auto_background_agents` sets the auto-background timeout to 120 seconds.
- `KAIROS` affects `AgentTool` schema visibility for `cwd` and also affects `assistantForceAsync`.
- `tengu_session_memory` is a distinct SessionMemory gate.
- `TEAMMEM` is the compile-time TeamMem gate.
- `tengu_herring_clock` continues to affect the runtime team-memory branch and telemetry.
- In `memdir.ts`, `KAIROS` plus `getKairosActive()` makes the daily-log prompt take precedence over the TeamMem path.
- `REACTIVE_COMPACT` suppresses proactive autocompact.
- `CONTEXT_COLLAPSE` suppresses part of the autocompact path when collapse mode is active.
- In `query.ts`, `CACHED_MICROCOMPACT`, `TOKEN_BUDGET`, `HISTORY_SNIP`, and `BG_SESSIONS` each control distinct context-management branches.
- `isTodoV2Enabled()` currently means:
  - force-enable Task V2 when `CLAUDE_CODE_ENABLE_TASKS` is true
  - otherwise Task V2 by default in interactive mode and TodoWrite by default in non-interactive mode

## Not Confirmed From Source

- Rollout for `KAIROS`, `TEAMMEM`, or SessionMemory.
- `/dream`, nightly distillation, or the final scope of any long-term memory product.
- One unified Task V2 product strategy across every entry point.

## Review Checklist

- Do not merge SessionMemory, TeamMem, and memdir into one system.
- Do not merge Task V2 and TodoWrite into one generic task concept.
- Do not turn KAIROS-related memory paths into rollout claims or a fully proven product loop.
