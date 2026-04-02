[简体中文](./README.md) | [English](./README.en.md)

# 02 Planning, Compaction, And Assistant

This chapter explains how Claude Code connects planning mode, plan files, compaction paths, and task-checklist layers into long-running sessions.

The public source mirror shows four mechanisms working together: `EnterPlanMode` / `ExitPlanMode` switch planning state, `utils/plans.ts` manages plan files and recovery, `query.ts` plus `services/compact/*` handle multi-level compaction, and `TodoWrite`, Task V2, and runtime tasks each keep separate storage and state.

## What You Should Understand After This Chapter

- what `Plan Mode` is, and what a plan file is
- why autocompact tries `sessionMemoryCompact` first
- why `TodoWrite`, Task V2, and runtime tasks need separate wording
- why compaction still needs attachments and plan file references afterward

## Key Files

- `_upstream/claude-code-sourcemap/restored-src/src/tools/EnterPlanModeTool/EnterPlanModeTool.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/ExitPlanModeTool/ExitPlanModeV2Tool.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/plans.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/attachments.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/query.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/services/compact/autoCompact.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/services/compact/compact.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/services/compact/sessionMemoryCompact.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/TodoWriteTool/TodoWriteTool.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/tasks.ts`

## Where To Start

- quick guide: [SIMPLE/README.en.md](./SIMPLE/README.en.md)
- deep dive: [DEEP/README.en.md](./DEEP/README.en.md)
- short comparison: [comparison.en.md](./comparison.en.md)
