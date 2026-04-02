[简体中文](./remote-bridge-and-session-gates.md) | [English](./remote-bridge-and-session-gates.en.md)

# Remote, Bridge, And Session Gates

This page tracks the gates around remote sessions, bridge paths, and CCR-related behavior.

## Key Source Files

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

## Confirmed From Source

- `BRIDGE_MODE` is the compile-time master switch for bridge capability.
- `tengu_ccr_bridge` is the Remote Control entitlement gate. `isBridgeEnabled()` also requires a claude.ai subscription.
- `getBridgeDisabledReason()` layers in profile-scope and `organizationUuid` checks.
- `tengu_bridge_repl_v2` only switches the REPL into the env-less bridge path. It does not prove bridge-wide availability.
- `tengu_bridge_repl_v2_cse_shim_enabled` controls the client-side `cse_* -> session_*` compatibility shim.
- `CCR_AUTO_CONNECT` plus `tengu_cobalt_harbor` controls the default for `remoteControlAtStartup`.
- `CCR_MIRROR` plus `tengu_ccr_mirror` controls outbound-only mirror mode.
- `initReplBridge.ts` explicitly states that the env-less path runs only when `!perpetual`; perpetual session continuity still falls back to the env-based path.
- `KAIROS` affects bridge CLI branches for `--session-id`, `--continue`, and resume-related flows.
- `tengu_cobalt_lantern` is currently confirmed only along GitHub-access reminder and remote-setup-adjacent paths.
- `tengu_surreal_dali` is currently confirmed only along scheduled or triggered remote-agent paths.
- In `entrypoints/agentSdkTypes.ts`, `connectRemoteControl()` and its related types are marked `@internal`, and the function body is still a `not implemented` stub.
- The same file states that one internal caller path skips the `tengu_ccr_bridge` gate and policy-limits check.

## Not Confirmed From Source

- Rollout of Remote Control for all users.
- Default-on status for the env-less bridge path across all builds.
- Availability of `connectRemoteControl()` as a public SDK API.
- Final public server-side transport, tag, or session contracts.

## Review Checklist

- Keep bridge and remote wording on the client-side or local outbound bridge layer.
- Keep `connectRemoteControl()` behind its `@internal` and stub boundary.
- Keep `tengu_bridge_repl_v2` as a REPL implementation branch, not a full-release claim.
