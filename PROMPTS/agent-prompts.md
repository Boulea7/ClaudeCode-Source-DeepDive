# Agent Prompts

主线程和子 agent 用的 prompt 不是完全一样的。

## 关键文件

- `restored-src/src/tools/AgentTool/forkSubagent.ts`
- `restored-src/src/tools/AgentTool/prompt.ts`
- `restored-src/src/tools/AgentTool/loadAgentsDir.ts`

## 可以确认的点

- fork child 会收到明确的 worker 指令
- child scope 被限制得很清楚
- 子 agent 不是随便继承全部行为，而是带有自己的运行约束

`forkSubagent.ts` 很值得读，因为它直接展示了 Claude Code 如何把一个 child 变成“执行型 worker”，而不是另一个自由聊天窗口。

