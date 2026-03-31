# 02 Planning, Compaction, And Assistant

这一章解释 Claude Code 如何把 Plan Mode、plan 文件、多路径 compact，以及 Todo / Task / runtime task 变成一组并行运行时机制。

## 这一章回答什么问题

- `Plan Mode` 到底是什么？
- 计划文件为什么能跨会话存在？
- `compact` 为什么不是一条单一路径？
- `TodoWrite`、Task V2、runtime task 分别是什么？

## 关键文件

- `restored-src/src/tools/EnterPlanModeTool/EnterPlanModeTool.ts`
- `restored-src/src/tools/ExitPlanModeTool/ExitPlanModeV2Tool.ts`
- `restored-src/src/utils/plans.ts`
- `restored-src/src/utils/attachments.ts`
- `restored-src/src/services/compact/autoCompact.ts`
- `restored-src/src/services/compact/compact.ts`
- `restored-src/src/services/compact/sessionMemoryCompact.ts`
- `restored-src/src/utils/tasks.ts`

## 阅读入口

- 快速版：[`SIMPLE/README.md`](./SIMPLE/README.md)
- 深度版：[`DEEP/README.md`](./DEEP/README.md)
- Agent 入口：[`AI-AGENT/agent-readme.txt`](./AI-AGENT/agent-readme.txt)
- 轻量比较：[`comparison.md`](./comparison.md)
