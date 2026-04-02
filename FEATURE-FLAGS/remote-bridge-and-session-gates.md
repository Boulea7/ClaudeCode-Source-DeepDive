[简体中文](./remote-bridge-and-session-gates.md) | [English](./remote-bridge-and-session-gates.en.md)

# Remote, Bridge, And Session Gates

这一页记录 remote session、bridge、CCR 相关 gate。

## 关键源码文件

- `_upstream/claude-code-sourcemap/restored-src/src/bridge/bridgeEnabled.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/bridge/initReplBridge.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/bridge/remoteBridgeCore.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/bridge/bridgeMain.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/remote/RemoteSessionManager.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/commands/bridge/bridge.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/commands/remote-setup/index.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/RemoteTriggerTool/RemoteTriggerTool.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/skills/bundled/scheduleRemoteAgents.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/background/remote/preconditions.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/entrypoints/agentSdkTypes.ts`

## 当前源码能确认的行为

- `BRIDGE_MODE` 是 bridge 能力的编译期总开关。
- `tengu_ccr_bridge` 是 Remote Control entitlement gate。`isBridgeEnabled()` 还会叠加 claude.ai subscription。
- `getBridgeDisabledReason()` 还会叠加 profile scope 与 `organizationUuid` 检查。
- `tengu_bridge_repl_v2` 只切换 REPL 的 env-less bridge path，不代表 bridge 整体可用性。
- `tengu_bridge_repl_v2_cse_shim_enabled` 控制 `cse_* -> session_*` 的客户端 compat shim。
- `CCR_AUTO_CONNECT` 与 `tengu_cobalt_harbor` 决定 remoteControlAtStartup 的默认值。
- `CCR_MIRROR` 与 `tengu_ccr_mirror` 控制 outbound-only mirror mode。
- `initReplBridge.ts` 明确写明 env-less path 只在 `!perpetual` 时启用；perpetual session continuity 仍回退 env-based path。
- `KAIROS` 会影响 bridge CLI 里的 `--session-id`、`--continue`、resume 相关分支。
- `tengu_cobalt_lantern` 当前只稳定坐实到 GitHub access 提示与 remote setup 相关路径。
- `tengu_surreal_dali` 当前只稳定坐实到 scheduled 或 triggered remote agent 路径。
- `entrypoints/agentSdkTypes.ts` 里 `connectRemoteControl()` 及其相关类型都标成 `@internal`，函数本体当前仍是 `not implemented` stub。
- 同文件注释写明某个 internal caller path 会跳过 `tengu_ccr_bridge` gate 和 policy-limits check。

## 当前源码不能确认的内容

- Remote Control 对所有用户的 rollout。
- env-less bridge path 在所有构建里的默认启用状态。
- `connectRemoteControl()` 作为公开 SDK API 的可用性。
- 服务端 transport、tag、session 模型的最终公开契约。

## 复核清单

- bridge 和 remote 继续写成客户端侧或本地出站桥接路径。
- `connectRemoteControl()` 继续保持 `@internal` 与 stub 边界。
- `tengu_bridge_repl_v2` 继续写成 REPL 实现分支，不写成全面发布。
- 中文页路径全部保持 `_upstream/...`。
