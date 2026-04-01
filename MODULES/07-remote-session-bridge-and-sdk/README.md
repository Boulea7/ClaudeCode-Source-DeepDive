[简体中文](./README.md) | [English](./README.en.md)

# 07 Remote Session, Bridge, And SDK

这一章解释 `remote/` 与 `bridge/` 如何分层。

## 读完这一章，你会更清楚什么

- `remote/` 负责什么
- `bridge/` 负责什么
- env-based 与 env-less 路径如何区分
- remote session 与本地会话怎样接起来

## 关键文件

- `_upstream/claude-code-sourcemap/restored-src/src/remote/RemoteSessionManager.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/remote/SessionsWebSocket.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/remote/sdkMessageAdapter.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/remote/remotePermissionBridge.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/bridge/initReplBridge.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/bridge/bridgeMain.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/bridge/replBridge.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/bridge/remoteBridgeCore.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/entrypoints/agentSdkTypes.ts`

## 从哪里开始读

- 快速版：[SIMPLE/README.md](./SIMPLE/README.md)
- 深度版：[DEEP/README.md](./DEEP/README.md)
- 轻量比较：[comparison.md](./comparison.md)
