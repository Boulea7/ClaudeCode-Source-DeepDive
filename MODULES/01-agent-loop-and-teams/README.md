# 01 Agent Loop And Teams

这一章讲 Claude Code 最像“运行时系统”的部分。

如果你最想知道它为什么不像一个只会开子任务的普通 agent，可以先读这一章。

## 读完这一章，你会更清楚什么

- 主线程和 worker 是怎么分工的？
- `AgentTool` 为什么不只是开一个子任务？
- task list、team、teammate 之间是什么关系？
- 为什么它看起来比普通 fan-out 更完整？

## 关键文件

- `restored-src/src/tools/AgentTool/AgentTool.tsx`
- `restored-src/src/tools/AgentTool/runAgent.ts`
- `restored-src/src/tools/AgentTool/forkSubagent.ts`
- `restored-src/src/tools/AgentTool/loadAgentsDir.ts`
- `restored-src/src/tasks/`
- `restored-src/src/coordinator/coordinatorMode.ts`

## 从哪里开始读

- 快速版：[`SIMPLE/README.md`](./SIMPLE/README.md)
- 深度版：[`DEEP/README.md`](./DEEP/README.md)
- Agent 入口：[`AI-AGENT/agent-readme.txt`](./AI-AGENT/agent-readme.txt)
- 轻量比较：[`comparison.md`](./comparison.md)
