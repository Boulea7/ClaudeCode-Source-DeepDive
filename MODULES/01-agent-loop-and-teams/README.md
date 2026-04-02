[简体中文](./README.md) | [English](./README.en.md)

# 01 Agent Loop And Teams

本章说明 Claude Code 如何把主会话、子 agent、后台任务和 team 协作放进同一套运行时。

公开镜像里，这条链路落在 `main.tsx`、`screens/REPL.tsx`、`QueryEngine.ts`、`query.ts`、`tools/AgentTool/*` 和 `tasks/*`。交互式入口与无头入口共享同一个 `query()` 回合循环。`AgentTool` 负责选择子 agent 路径。`runAgent()` 负责真正执行子会话。`tasks/*` 负责把本地 agent、远端 agent、主会话后台任务、shell 和同进程 teammate 统一到任务表示层。

## 读完这一章，你会更清楚什么

- `main.tsx -> REPL.tsx -> query.ts` 与 `main.tsx -> QueryEngine.ts -> query.ts` 的分工
- `AgentTool`、`runAgent()`、`forkSubagent.ts` 各自解决什么问题
- fork worker 与普通 subagent 的继承关系为什么不能混写
- `local_agent`、`remote_agent`、`in_process_teammate`、`main-session` 在任务层如何落位

## 关键文件

- `_upstream/claude-code-sourcemap/restored-src/src/main.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/screens/REPL.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/QueryEngine.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/query.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/AgentTool.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/runAgent.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/forkSubagent.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/resumeAgent.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tasks/`

## 从哪里开始读

- 快速版：[SIMPLE/README.md](./SIMPLE/README.md)
- 深度版：[DEEP/README.md](./DEEP/README.md)
- 轻量比较：[comparison.md](./comparison.md)
