[简体中文](./agent-memory-compact-gates.md) | [English](./agent-memory-compact-gates.en.md)

# Agent, Memory, And Compact Gates

这一页记录 agent、memory、compact、task layer 的 gate。

## 关键源码文件

- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/AgentTool.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/runAgent.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/forkSubagent.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/services/SessionMemory/sessionMemory.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/memdir/memdir.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/memdir/paths.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/memdir/teamMemPaths.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/services/compact/autoCompact.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/query.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/tasks.ts`

## 当前源码能确认的行为

- `FORK_SUBAGENT` 会让省略 `subagent_type` 的 Agent 调用进入 fork path。
- `FORK_SUBAGENT` 打开时，`AgentTool` schema 会隐藏 `run_in_background`。
- `CLAUDE_CODE_DISABLE_BACKGROUND_TASKS` 会整体禁用后台任务能力。
- `CLAUDE_AUTO_BACKGROUND_TASKS` 或 `tengu_auto_background_agents` 会把自动后台化超时设成 120 秒。
- `KAIROS` 会影响 `AgentTool` schema 中 `cwd` 的可见性，也会影响 `assistantForceAsync`。
- `tengu_session_memory` 是 SessionMemory 的单独 gate。
- `TEAMMEM` 是 TeamMem 的编译期开关。
- `tengu_herring_clock` 会继续影响 team memory 的运行时分支和 telemetry。
- `memdir.ts` 里 `KAIROS` 且 `getKairosActive()` 为真时，daily-log prompt 优先于 TeamMem 路径。
- `REACTIVE_COMPACT` 会抑制 proactive autocompact。
- `CONTEXT_COLLAPSE` 会在启用时抑制 autocompact 的部分路径。
- `query.ts` 里 `CACHED_MICROCOMPACT`、`TOKEN_BUDGET`、`HISTORY_SNIP`、`BG_SESSIONS` 各自控制不同 context 管理分支。
- `isTodoV2Enabled()` 的当前规则是：
  - `CLAUDE_CODE_ENABLE_TASKS` 为真时强制开启 Task V2
  - 否则 interactive 默认 Task V2，non-interactive 默认 TodoWrite

## 当前源码不能确认的内容

- `KAIROS`、`TEAMMEM`、`SessionMemory` 的 rollout。
- `/dream`、nightly distillation、长期记忆产品化范围。
- 所有入口下 Task V2 的统一产品策略。

## 复核清单

- SessionMemory、TeamMem、memdir 不混写成同一个系统。
- Task V2 与 TodoWrite 不混写成一个 task 概念。
- `KAIROS` 相关 memory 路径不写成 rollout 或完整产品闭环。
- 中文页路径全部保持 `_upstream/...`。
