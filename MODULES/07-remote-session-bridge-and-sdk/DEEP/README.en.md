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
- `_upstream/claude-code-sourcemap/restored-src/src/bridge/initReplBridge.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/bridge/replBridge.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/bridge/remoteBridgeCore.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/bridge/bridgeMain.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/bridge/sessionRunner.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/cli/print.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/entrypoints/agentSdkTypes.ts`

## Main Points

- `remote/` attaches to an existing remote session and handles message and permission round-trips.
- `bridge/` connects a local REPL or child CLI to remote-control paths.
- env-based and env-less bridge paths are different runtime strategies.
- `bridgeMain.ts` and `sessionRunner.ts` should not be collapsed into the same role.
- `connectRemoteControl()` still needs conservative wording because the current mirror keeps it as a stub.

## Conservative Boundaries

- keep `/bridge`, `worker_epoch`, and related fields as client-visible contract clues
- keep `headless`, `standalone`, and child-CLI wording separated
- keep `remote isolation` limited to client-side mode/schema wording unless stronger source evidence is re-read

## Read Next

- [README.en.md](../README.en.md)
- [comparison.en.md](../comparison.en.md)
