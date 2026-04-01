[简体中文](./README.md) | [English](./README.en.md)

# 07 Remote Session, Bridge, And SDK

This chapter explains how `remote/` and `bridge/` are split into separate layers.

## What You Should Understand After This Chapter

- what `remote/` handles
- what `bridge/` handles
- how env-based and env-less paths differ
- how remote sessions connect back to local sessions

## Key Files

- `_upstream/claude-code-sourcemap/restored-src/src/remote/RemoteSessionManager.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/remote/SessionsWebSocket.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/remote/sdkMessageAdapter.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/remote/remotePermissionBridge.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/bridge/initReplBridge.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/bridge/bridgeMain.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/bridge/replBridge.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/bridge/remoteBridgeCore.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/entrypoints/agentSdkTypes.ts`

## Where To Start

- quick guide: [SIMPLE/README.en.md](./SIMPLE/README.en.md)
- deep dive: [DEEP/README.en.md](./DEEP/README.en.md)
- short comparison: [comparison.en.md](./comparison.en.md)
