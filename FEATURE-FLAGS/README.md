[简体中文](./README.md) | [English](./README.en.md)

# FEATURE-FLAGS

这一组文档记录会改写运行路径、prompt 路径、memory 路径和 remote 路径的 gate。

## 阅读顺序

1. [runtime-and-prompt-gates.md](./runtime-and-prompt-gates.md)
2. [agent-memory-compact-gates.md](./agent-memory-compact-gates.md)
3. [remote-bridge-and-session-gates.md](./remote-bridge-and-session-gates.md)

## 写法边界

- `feature()` 代表编译期开关。
- GrowthBook 和 env 代表运行时开关。
- 代码里出现 gate 代表分支存在，不代表已经 rollout。
- 代码里出现名字，不代表已经是公开产品命名。
- `Buddy`、`KAIROS`、`PROACTIVE`、`voice`、`bridge`、`remote` 保持保守表述。

## 本轮直接回读的主干源码

- `_upstream/claude-code-sourcemap/restored-src/src/constants/prompts.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/screens/REPL.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/QueryEngine.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/AgentTool.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/forkSubagent.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/services/SessionMemory/sessionMemory.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/memdir/memdir.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/memdir/paths.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/memdir/teamMemPaths.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/services/compact/autoCompact.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/tasks.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/bridge/bridgeEnabled.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/bridge/initReplBridge.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/bridge/bridgeMain.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/entrypoints/agentSdkTypes.ts`
