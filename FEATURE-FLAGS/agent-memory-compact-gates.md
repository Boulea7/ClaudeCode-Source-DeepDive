# Agent, Memory, And Compact Gates

## 这部分关注什么 gate

这一页主要整理：

- agent spawn / fork / teammate 相关 gate
- SessionMemory、memdir、team memory 相关 gate
- compact、Task V2、Plan Mode 周边的 gate 与 env 开关

## 关键文件

- `restored-src/src/tools/AgentTool/AgentTool.tsx`
- `restored-src/src/tools/AgentTool/runAgent.ts`
- `restored-src/src/tools/AgentTool/forkSubagent.ts`
- `restored-src/src/utils/agentSwarmsEnabled.ts`
- `restored-src/src/services/SessionMemory/sessionMemory.ts`
- `restored-src/src/services/extractMemories/extractMemories.ts`
- `restored-src/src/memdir/memdir.ts`
- `restored-src/src/memdir/paths.ts`
- `restored-src/src/memdir/teamMemPaths.ts`
- `restored-src/src/services/teamMemorySync/index.ts`
- `restored-src/src/services/teamMemorySync/watcher.ts`
- `restored-src/src/services/autoDream/autoDream.ts`
- `restored-src/src/utils/sessionFileAccessHooks.ts`
- `restored-src/src/services/compact/autoCompact.ts`
- `restored-src/src/query.ts`
- `restored-src/src/utils/tasks.ts`
- `restored-src/src/tools/TodoWriteTool/TodoWriteTool.ts`
- `restored-src/src/tools/TaskUpdateTool/TaskUpdateTool.ts`

## 代码里能确认的行为

### `FORK_SUBAGENT`

- 省略 `subagent_type` 时，fork gate 开启会走 fork path，而不是默认 general-purpose。
- `AgentTool` schema 还会据此隐藏 `run_in_background`。
- 文档应写成“fork 会改变默认 spawn 语义”，不是普通 agent type。

### `tengu_auto_background_agents` + `CLAUDE_AUTO_BACKGROUND_TASKS`

- `AgentTool.tsx` 里会把前台 agent 在 120 秒后自动后台化。
- 同时 `CLAUDE_CODE_DISABLE_BACKGROUND_TASKS` 会整体禁用后台化能力。

### `AGENT_TRIGGERS` / `AGENT_TRIGGERS_REMOTE`

- 相关 gate 会影响 scheduler / remote agent 触发链。
- 当前更适合写成“agent 触发型能力有独立 gate”，不要默认当成常规 subagent 行为。

### `WORKFLOW_SCRIPTS` / `MONITOR_TOOL`

- `tasks.ts`、`PermissionRequest.tsx`、`AgentTool/runAgent.ts` 都有对应 gate。
- 这说明 workflow / monitor 属于条件编译进来的可选工具，不是默认恒定存在。

### `TRANSCRIPT_CLASSIFIER` / `BASH_CLASSIFIER`

- 这些 gate 不只是权限层开关，也会影响 `AgentTool`、Plan Mode 退出、auto mode 恢复、classifier approval。
- 当前更适合写成“auto mode 与审批链的 gated safety path”。

### `tengu_session_memory`

- `services/SessionMemory/sessionMemory.ts` 用它决定 SessionMemory 功能是否开启。
- 这说明 SessionMemory 是单独 gate 的，不应与 durable memory 一起写成永远同开。

### `TEAMMEM` + `tengu_herring_clock`

- `memdir/memdir.ts`、`teamMemPaths.ts`、`paths.ts` 都有 team memory 相关分支。
- `TEAMMEM` 是编译期开关；`tengu_herring_clock` 还会影响运行时是否进入 team memory 分支。
- `setup.ts` 和 `teamMemorySync/watcher.ts` 还能确认本地同步链：先 initial pull，再启动 watcher；`sessionFileAccessHooks.ts` 会在 TeamMem 写后显式通知同步层。

### `KAIROS` 对 memory 的影响

- `memdir/memdir.ts` 在 `feature('KAIROS') && getKairosActive()` 时会切到 daily-log prompt。
- `memdir/paths.ts` 与 `memdir/memdir.ts` 的注释都把 nightly `/dream`、distill、日志到 `MEMORY.md` 的关系写成 prompt / 注释层线索。
- 这里能确认的是：KAIROS 会改变“新 memory 写到哪里”的提示逻辑；`MEMORY.md` 仍会被当成 distilled index 读入上下文。
- 当前还能确认另一条边界：`autoDream` 会在 `getKairosActive()` 时直接关闭，所以不能把 KAIROS daily-log 与当前可见的 `autoDream` 机制混成同一条实现链。
- `skills/bundled/index.ts` 里还能看到：`feature('KAIROS') || feature('KAIROS_DREAM')` 时会尝试 `registerDreamSkill()`，说明 `/dream` 至少有 skill 注册点，不只是注释里的名字。
- 不能把它直接写成 nightly distillation 已经在当前公开构建里稳定上线，更不能写成完整长期记忆产品已发布。

### `tengu_coral_fern` / `tengu_moth_copse`

- `memdir/memdir.ts` 里：
  - `tengu_coral_fern` 控制“Searching past context”这一段是否出现。
  - `tengu_moth_copse` 控制是否跳过 `MEMORY.md` index 写法说明。
- `claudemd.ts` 里还能看到：`tengu_moth_copse` 打开后，`AutoMem/TeamMem` 入口索引会从 system prompt 注入集合中过滤掉，改由 relevant-memory prefetch 去 surfaced topic files。

### `tengu_passport_quail` / `tengu_slate_thimble` / `tengu_bramble_lintel`

- 这些分支分别出现在 auto memory path、durable extraction、extractMemories 频率或策略上。
- 当前可以写成 durable memory 的目录 / 写入策略仍受运行时 gate 控制。

### `REACTIVE_COMPACT` / `CONTEXT_COLLAPSE` / `CACHED_MICROCOMPACT` / `TOKEN_BUDGET` / `HISTORY_SNIP` / `BG_SESSIONS`

- `query.ts` 和 `services/compact/autoCompact.ts` 都显示这几条是独立层：
  - `REACTIVE_COMPACT` 可抑制 proactive autocompact。
  - `CONTEXT_COLLAPSE` 会接管一部分上下文管理。
  - `CACHED_MICROCOMPACT` 有延迟反馈链。
  - `TOKEN_BUDGET` 会改变 continuation。
  - `HISTORY_SNIP`、`BG_SESSIONS` 各自控制不同压缩 / 背景附件行为。
- 它们不能被合并成“单一 compact 开关”。

### Task V2 / TodoWrite 切换

- 这里不完全是 `feature(...)`，而是 `isTodoV2Enabled()` 的运行时切换逻辑：
  - 交互式默认 Task V2。
  - 非交互式默认 TodoWrite。
  - `CLAUDE_CODE_ENABLE_TASKS` 可以强制打开 Task V2。
- 文档要把它写成“运行时策略开关”，不要混成 runtime task。

## 不能确认的发布状态

- 这份镜像能证明相关分支存在，但不能证明这些 gate 在当前正式版全都打开。
- `KAIROS` 与 memory 的关系，目前只能确认 daily-log prompt / assistant-mode 分支；nightly `/dream`、distillation、append-only log 更像 prompt / 注释里的运行线索，不能确认完整公开范围。
- `autoDream` 是 opportunistic consolidation 机制，不是固定 nightly job；同时它在 `getKairosActive()` 时会关闭，所以不能拿它当作 KAIROS daily-log 的直接后台实现。
- `/dream` 这条线现在能确认到 skill 注册点、后台 autoDream 链路和 UI 文案，但 `dream.js` 实现文件这轮仍未在当前镜像里复核到，因此手动 `/dream` 的完整执行细节仍不能写死。
- TeamMem 的本地同步链已经能确认到 `startup pull + watcher + 写后通知`，但 push 仍有 debounce / suppression / shutdown best-effort 语义，不能写成强一致同步承诺。
- Task V2 的默认启用逻辑在交互式会话里可见，但不能仅凭静态代码推出所有入口的一致产品策略。

## 容易误写的点

- 不要把 SessionMemory、extractMemories、memdir 写成“同一 memory 系统的不同层级开关”。
- 不要把 `REACTIVE_COMPACT`、`CONTEXT_COLLAPSE` 写成“同一个实验名字的别名”。
- 不要把 `TEAMMEM` 写成“所有用户都默认拥有的 team memory”。
- 不要把 TodoWrite / Task V2 / runtime task 混成一种“Task”。
- 不要把 `KAIROS` daily-log 路径写成“已经能从源码证实 nightly distillation 完整跑通”。
- 不要把 `autoDream` 写成“KAIROS nightly /dream 的已证实后台实现”。

## 推荐阅读顺序

1. `restored-src/src/tools/AgentTool/AgentTool.tsx`
2. `restored-src/src/utils/agentSwarmsEnabled.ts`
3. `restored-src/src/services/SessionMemory/sessionMemory.ts`
4. `restored-src/src/memdir/memdir.ts`
5. `restored-src/src/memdir/paths.ts`
6. `restored-src/src/services/extractMemories/extractMemories.ts`
7. `restored-src/src/services/compact/autoCompact.ts`
8. `restored-src/src/query.ts`
9. `restored-src/src/utils/tasks.ts`
