[简体中文](./README.md) | [English](./README.en.md)

# 01 Agent Loop And Teams

这一章聚焦 Claude Code 最接近“运行时系统”的部分。

如果你最关心主线程、worker、task、team 如何接到同一条运行链上，这一章最适合先读。

## 读完这一章，你会更清楚什么

- 主线程和 worker 如何分工
- `AgentTool` 在编排链中的位置
- task、team、teammate 如何进入同一套状态层
- fork subagent 为什么要单独看

## 关键文件

- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/AgentTool.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/runAgent.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/forkSubagent.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/loadAgentsDir.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tasks/`
- `_upstream/claude-code-sourcemap/restored-src/src/coordinator/coordinatorMode.ts`

## 从哪里开始读

- 快速版：[SIMPLE/README.md](./SIMPLE/README.md)
- 深度版：[DEEP/README.md](./DEEP/README.md)
- 轻量比较：[comparison.md](./comparison.md)
