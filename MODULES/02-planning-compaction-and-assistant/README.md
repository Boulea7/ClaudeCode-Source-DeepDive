# 02 Planning, Compaction, And Assistant

这一章解释 Claude Code 如何把“先规划、再执行、再压缩上下文”做成一条连续流程。

## 这一章回答什么问题

- `Plan Mode` 到底是什么？
- 计划文件为什么能跨会话存在？
- `compact` 和计划文件之间是什么关系？
- `QueryEngine` 在这里扮演什么角色？

## 关键文件

- `restored-src/src/tools/EnterPlanModeTool/EnterPlanModeTool.ts`
- `restored-src/src/tools/ExitPlanModeTool/ExitPlanModeV2Tool.ts`
- `restored-src/src/commands/plan/plan.tsx`
- `restored-src/src/utils/plans.ts`
- `restored-src/src/services/compact/compact.ts`
- `restored-src/src/QueryEngine.ts`

## 阅读入口

- 快速版：[`SIMPLE/README.md`](./SIMPLE/README.md)
- 深度版：[`DEEP/README.md`](./DEEP/README.md)
- Agent 入口：[`AI-AGENT/agent-readme.txt`](./AI-AGENT/agent-readme.txt)
- 轻量比较：[`comparison.md`](./comparison.md)

