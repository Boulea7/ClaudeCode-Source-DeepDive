[简体中文](./README.md) | [English](./README.en.md)

# 02 Planning, Compaction, And Assistant

本章说明 Claude Code 如何把计划态、plan 文件、compact 路径和任务清单层接进长会话运行时。

公开镜像显示四条相关机制同时存在：`EnterPlanMode` / `ExitPlanMode` 负责切换计划态，`utils/plans.ts` 负责 plan 文件与恢复，`query.ts` 与 `services/compact/*` 负责多级 compact，`TodoWrite`、Task V2、runtime task 则各有独立存储与状态层。

## 读完这一章，你会更清楚什么

- `Plan Mode` 是什么状态，plan 文件又是什么对象
- 自动 compact 为什么优先尝试 `sessionMemoryCompact`
- `TodoWrite`、Task V2、runtime task 为什么要分开写
- compact 后为什么还需要 attachment 和 plan file reference

## 关键文件

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

## 从哪里开始读

- 快速版：[SIMPLE/README.md](./SIMPLE/README.md)
- 深度版：[DEEP/README.md](./DEEP/README.md)
- 轻量比较：[comparison.md](./comparison.md)
