[简体中文](./README.md) | [English](./README.en.md)

# 02 Planning, Compaction, And Assistant

This chapter explains how `Plan Mode`, plan files, multiple compaction paths, and Todo / Task / runtime-task layers connect to the same long-running conversation chain.

## What You Should Understand After This Chapter

- what `Plan Mode` means as a runtime state
- why plan files can survive across turns and resumes
- why `compact` is split across multiple paths
- what `TodoWrite`, Task V2, and runtime tasks each handle

## Key Files

- `_upstream/claude-code-sourcemap/restored-src/src/tools/EnterPlanModeTool/EnterPlanModeTool.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/ExitPlanModeTool/ExitPlanModeV2Tool.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/plans.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/attachments.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/services/compact/autoCompact.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/services/compact/compact.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/services/compact/sessionMemoryCompact.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/tasks.ts`

## Where To Start

- quick guide: [SIMPLE/README.en.md](./SIMPLE/README.en.md)
- deep dive: [DEEP/README.en.md](./DEEP/README.en.md)
- short comparison: [comparison.en.md](./comparison.en.md)
