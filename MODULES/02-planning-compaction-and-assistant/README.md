[简体中文](./README.md) | [English](./README.en.md)

# 02 Planning, Compaction, And Assistant

这一章解释 `Plan Mode`、plan 文件、多路径 compact，以及 Todo / Task / runtime task 如何接到同一条长会话链上。

## 读完这一章，你会更清楚什么

- `Plan Mode` 在运行时里是什么状态
- plan 文件为什么能跨会话保留
- `compact` 为什么会分成多条路径
- `TodoWrite`、Task V2、runtime task 各自负责什么

## 关键文件

- `_upstream/claude-code-sourcemap/restored-src/src/tools/EnterPlanModeTool/EnterPlanModeTool.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/ExitPlanModeTool/ExitPlanModeV2Tool.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/plans.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/attachments.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/services/compact/autoCompact.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/services/compact/compact.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/services/compact/sessionMemoryCompact.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/tasks.ts`

## 从哪里开始读

- 快速版：[SIMPLE/README.md](./SIMPLE/README.md)
- 深度版：[DEEP/README.md](./DEEP/README.md)
- 轻量比较：[comparison.md](./comparison.md)
