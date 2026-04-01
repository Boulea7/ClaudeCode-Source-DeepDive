# Remote, Bridge, And Session Gates

## 这部分关注什么 gate

这一页只整理：

- 远端 session 客户端
- bridge / Remote Control
- CCR / env-less / mirror / remote backend

这些能力在源码里确实有分支，但大多数都不能直接外推为“已公开默认能力”。

## 关键文件

- `restored-src/src/remote/RemoteSessionManager.ts`
- `restored-src/src/bridge/bridgeEnabled.ts`
- `restored-src/src/bridge/initReplBridge.ts`
- `restored-src/src/bridge/replBridge.ts`
- `restored-src/src/bridge/remoteBridgeCore.ts`
- `restored-src/src/bridge/bridgeMain.ts`
- `restored-src/src/bridge/sessionRunner.ts`
- `restored-src/src/cli/print.ts`
- `restored-src/src/main.tsx`
- `restored-src/src/commands/bridge/bridge.tsx`
- `restored-src/src/commands/remote-setup/index.ts`
- `restored-src/src/entrypoints/agentSdkTypes.ts`
- `restored-src/src/tools/RemoteTriggerTool/RemoteTriggerTool.ts`
- `restored-src/src/skills/bundled/scheduleRemoteAgents.ts`
- `restored-src/src/utils/background/remote/preconditions.ts`

## 代码里能确认的行为

### `BRIDGE_MODE`

- `bridge/bridgeEnabled.ts` 用它做编译期总开关。
- 关闭时，bridge 相关字符串和路径会被裁掉。
- 这说明 bridge 不是默认恒定存在的运行时。

### `tengu_ccr_bridge`

- `isBridgeEnabled()` / `isBridgeEnabledBlocking()` 会用它判断 Remote Control entitlement。
- 还会叠加 Claude.ai subscription / OAuth profile scope / organizationUuid。
- 文档应写成“客户端有 entitlement gate”，不是“所有登录用户都能用”。

### `tengu_bridge_repl_v2`

- `bridgeEnabled.ts` 里它控制 env-less REPL bridge path。
- 注释明确说它只决定 REPL 用哪条实现，不等于 bridge 能力整体是否可用。
- 同一段注释还写明 daemon / `--print` 路径仍停在 env-based，不跟这条 gate 一起切。

### `tengu_bridge_repl_v2_cse_shim_enabled`

- `bridgeEnabled.ts` 里它控制 `cse_* -> session_*` 的 compat shim 是否启用。
- 默认值是 `true`，更接近“客户端兼容 shim 默认保持开启，直到明确下线”。
- 当前能确认的是客户端 ID 兼容分支存在，不能反推服务端当前接受哪些 tag。

### `tengu_cobalt_harbor` + `CCR_AUTO_CONNECT`

- 这组逻辑决定 Remote Control 是否默认自动连接。
- 用户显式配置仍可覆盖默认值。

### `tengu_ccr_mirror` + `CCR_MIRROR`

- 这组逻辑控制 outbound-only 的 mirror mode。
- 它和双向 Remote Control 不是同一个东西。

### `tengu_remote_backend`

- `main.tsx` 里可见 remote backend TUI gate。
- 当前更准确的写法是：它主要影响 `claude --remote` 进入 TUI 时的入口判定，不能外推成完整 remote backend 产品形态。

### `KAIROS` 对 bridge CLI 形态的影响

- `bridgeMain.ts` 和 `initReplBridge.ts` 里都能看到 `feature('KAIROS')` 对 `--session-id`、`--continue`、resume / perpetual bridge 的控制。
- 更稳妥的说法是：某些 session continuity / assistant-style bridge 行为仍受 KAIROS gate 约束。

### `tengu_cobalt_lantern`

- 这个 key 主要出现在 `remote-setup`、`scheduleRemoteAgents` 和 background remote preconditions 中。
- 当前更准确的边界是：它会影响 GitHub repo access 提示与 token-sync 路径，不等于整个 remote agent 功能总开关。

### `tengu_surreal_dali`

- 这个 key 主要落在 `RemoteTriggerTool` 和 `scheduleRemoteAgents` 路径上。
- 当前更准确的边界是：它更接近 scheduled / triggered remote agents 的 rollout gate，不是 bridge 核心 transport 开关。

### `CHICAGO_MCP`

- `query.ts`、`query/stopHooks.ts`、`services/mcp/config.ts`、`services/mcp/client.ts`、`utils/computerUse/*` 里都能看到 `CHICAGO_MCP` 分支。
- 当前更稳妥的写法是：它更像 computer-use MCP 的 reserved-name、in-process server、tool override 和 wrapper 分支，公开状态不能仅凭源码判断。

### `agentSdkTypes` 内部桥接入口

- `entrypoints/agentSdkTypes.ts` 里有 `@internal` helper 明确写着会跳过 `tengu_ccr_bridge` gate 和 policy-limits check。
- 这说明源码里存在 pre-entitled internal caller 路径。
- 更稳妥的写法是：这是内部桥接接线面，不能拿来反推公开 SDK 默认 entitlement。

## 不能确认的发布状态

- `RemoteSessionManager` 能证明已有 session 的客户端层存在，但不能证明所有用户都可创建对应远端 session。
- `bridge/` 里 env-based / env-less / standalone worker 三条路径都存在，但默认启用条件仍受 build / entitlement / runtime gate 控制；当前更准确的运行时分层是 `initReplBridge()` 负责 REPL 包装，`initBridgeCore()` 负责 env-based core，`initEnvLessBridgeCore()` 负责 env-less core，`runBridgeHeadless()` 负责 daemon worker 入口。
- v1 `HybridTransport` 与 v2 `SSETransport + CCRClient` 能确认是客户端 transport 形态，不能写成服务端架构承诺。
- `entrypoints/agentSdkTypes.ts` 里虽然有 remote-control 类型与注释，但当前镜像中的 `connectRemoteControl()` 仍是 stub，不能把它写成已证实可用的公开 SDK 方法。
- `query.enableRemoteControl` 这轮也继续缩小了边界：在当前镜像范围里，只能在 `entrypoints/agentSdkTypes.ts` 与 `bridge/initReplBridge.ts` 的注释里看到这个名字，没有看到同名字段、方法或 runtime 开关实现，因此不能把它写成已完整坐实的公开 SDK API。
- `remote/` 当前更适合写成“已有 CCR session 的 attach / subscribe / message-adapter 层”；这轮没有看到把它直接接成 `connectRemoteControl()` SDK glue 的证据。

## 容易误写的点

- 不要把 `remote/` 写成“远端执行平台本体”。
- 不要把 `bridge/` 写成“本地服务端实现”；当前更准确是出站桥接层。
- 不要把 `tengu_bridge_repl_v2` 写成“Remote Control v2 已全面发布”。
- 不要把 `session_*` / `cse_*` compat shim 写成服务端事实。
- 不要把 `agentSdkTypes` 里的 internal pre-entitled helper 写成“公开 SDK 默认跳过 entitlement gate”。

## 推荐阅读顺序

1. `restored-src/src/bridge/bridgeEnabled.ts`
2. `restored-src/src/remote/RemoteSessionManager.ts`
3. `restored-src/src/bridge/initReplBridge.ts`
4. `restored-src/src/bridge/replBridge.ts`
5. `restored-src/src/bridge/remoteBridgeCore.ts`
6. `restored-src/src/bridge/bridgeMain.ts`
7. `restored-src/src/bridge/sessionRunner.ts`
8. `restored-src/src/cli/print.ts`
