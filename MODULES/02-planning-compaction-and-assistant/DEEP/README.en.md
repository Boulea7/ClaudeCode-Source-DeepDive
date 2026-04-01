[简体中文](./README.md) | [English](./README.en.md)

# Deep Dive: Planning, Compaction, And Assistant

This chapter explains how `Plan Mode`, plan files, compaction paths, and task/todo layers connect to long-running conversations.

## What This Chapter Covers

- `Plan Mode` as a permission-state change
- plan files as separate artifacts
- multiple compaction paths
- the split between `TodoWrite`, Task V2, and runtime tasks

## Key Source Files

- `_upstream/claude-code-sourcemap/restored-src/src/tools/EnterPlanModeTool/EnterPlanModeTool.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/ExitPlanModeTool/ExitPlanModeV2Tool.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/plans.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/attachments.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/services/compact/autoCompact.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/services/compact/compact.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/services/compact/sessionMemoryCompact.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/tasks.ts`

## Main Points

- `Plan Mode` changes permission state and depends on attachments to stay visible across long conversations.
- plan files are managed separately from the mode switch itself.
- `autoCompactIfNeeded()` tries session-memory compaction before falling back to full compaction.
- `TodoWrite`, Task V2, and runtime tasks are three different layers.
- `TaskOutputTool` and `TaskStopTool` target runtime tasks, not Task V2 JSON records.

## Conservative Boundaries

- `sessionMemoryCompact` clearly reinjects `plan_file_reference`, but broader reinjection parity with full compaction should stay conservative.
- the first upstream point that materializes plan content is still narrower than “entering Plan Mode”.
- rollout status for cached microcompaction and related gates cannot be inferred from static source alone.

## Read Next

- [README.en.md](../README.en.md)
- [comparison.en.md](../comparison.en.md)
