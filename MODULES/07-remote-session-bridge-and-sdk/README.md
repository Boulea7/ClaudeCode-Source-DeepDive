# 07 Remote Session, Bridge, And SDK

这一章解释 Claude Code 如何把“远端 session 客户端”和“本地 bridge/control layer”分开建模。

## 这一章回答什么问题

- `remote/` 目录里到底有什么？
- `bridge/` 为什么不是本地服务端？
- env-based 和 env-less 是什么关系？
- remote session 和本地会话是怎样接起来的？

## 关键文件

- `restored-src/src/remote/RemoteSessionManager.ts`
- `restored-src/src/remote/SessionsWebSocket.ts`
- `restored-src/src/remote/sdkMessageAdapter.ts`
- `restored-src/src/remote/remotePermissionBridge.ts`
- `restored-src/src/bridge/initReplBridge.ts`
- `restored-src/src/bridge/bridgeMain.ts`
- `restored-src/src/bridge/replBridge.ts`
- `restored-src/src/bridge/remoteBridgeCore.ts`

## 阅读入口

- 快速版：[`SIMPLE/README.md`](./SIMPLE/README.md)
- 深度版：[`DEEP/README.md`](./DEEP/README.md)
- Agent 入口：[`AI-AGENT/agent-readme.txt`](./AI-AGENT/agent-readme.txt)
- 轻量比较：[`comparison.md`](./comparison.md)
