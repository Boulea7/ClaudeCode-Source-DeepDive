[简体中文](./README.md) | [English](./README.en.md)

# Deep Dive: Remote Session, Bridge, And SDK

This chapter separates the attach-side remote session client from the local bridge layer.

## What This Chapter Covers

- what `remote/` does
- what `bridge/` does
- how env-based and env-less paths differ
- how child CLI execution relates to bridge paths

## Key Source Files

- `_upstream/claude-code-sourcemap/restored-src/src/remote/RemoteSessionManager.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/remote/SessionsWebSocket.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/remote/sdkMessageAdapter.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/remote/remotePermissionBridge.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/bridge/initReplBridge.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/bridge/replBridge.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/bridge/remoteBridgeCore.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/bridge/bridgeMain.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/bridge/replBridgeTransport.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/bridge/sessionRunner.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/cli/print.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/entrypoints/agentSdkTypes.ts`

## Execution Flow

### 1. `remote/` is the attach-side client for an existing session

The current mirror supports a narrower and clearer description of `remote/`:

- it connects around an existing `sessionId`
- it subscribes to remote messages
- it sends user messages back out
- it handles remote permission request and response traffic
- it adapts remote SDK messages into local REPL or UI-facing shapes

That is why `remote/` should stay described as the client side of an existing remote session, not as the full remote platform.

### 2. `remote/` does not register environments or spawn local workers

Another important boundary is negative, but still source-backed: the `remote/` layer is not where environment registration, work polling, or local child-CLI spawning happens.

Those responsibilities live in `bridge/`.

Keeping that split explicit prevents the most common documentation drift in this area.

### 3. `bridge/` is the local bridge layer

The safer description for `bridge/` in the current mirror is a local bridge layer that connects a local REPL or child CLI to remote-control paths.

This layer is easier to understand when split into:

- env-based paths
- env-less paths
- standalone or headless worker paths

That is already enough to show it is more than a thin adapter and also different from the attach-side `remote/` client.

### 4. Env-based and env-less are different runtime strategies

The current source supports two distinct bridge strategies.

The env-based path is built around environment registration, work polling, and work acknowledgement before transport setup.

The env-less path goes through code-session creation and bridge credential exchange before transport setup.

The key conservative wording here is:

- env-less is an implementation switch for the REPL bridge path
- it is not proof of one universal transport version across every bridge surface

### 5. `bridgeMain.ts` and `sessionRunner.ts` reach a local child CLI

`bridgeMain.ts` and `sessionRunner.ts` show another side of the bridge system: some paths end up launching a local `claude --print --sdk-url --session-id ...` child process and then bridging over stdin/stdout.

That is the strongest source-backed reason not to collapse `bridge/` into “message forwarding only”.

It also explains why `bridgeMain.ts`, `sessionRunner.ts`, and `cli/print.ts` should not be treated as the same role.

### 6. Transport shapes are client-side evidence, not server guarantees

The current mirror supports at least a v1 and v2 client-side transport story.

That is useful for understanding how the client connects and resumes. It is not enough to turn the docs into server-architecture claims.

The same caution applies to fields such as `/bridge`, `worker_epoch`, and session-ID compatibility tags. They are better described as client-visible contract clues and compatibility branches.

## Why This Layer Matters

The separation between `remote/` and `bridge/` explains why Claude Code can treat:

- remote session attachment
- permission round-trips
- local REPL bridging
- child CLI execution
- resume and reconnect behavior

as related but distinct runtime concerns.

That separation also makes the documentation safer, because it reduces the temptation to guess server structure from client code alone.

## Conservative Boundaries

- keep `/bridge`, `worker_epoch`, and related fields as client-visible contract clues
- keep `headless`, `standalone`, and child-CLI wording separated
- keep `connectRemoteControl()` conservative because the current mirror still leaves it as a stub
- keep `remote isolation` limited to client-side mode and schema wording unless stronger source evidence is re-read
- keep env-less wording scoped to the REPL bridge path unless another surface is re-verified in source

## Read Next

- [README.en.md](../README.en.md)
- [comparison.en.md](../comparison.en.md)
