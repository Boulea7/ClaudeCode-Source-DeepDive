# 07 Remote Session, Bridge, And SDK

这一章解释 Claude Code 如何离开单一本地终端，进入 bridge、remote session 和 SDK 场景。

## 这一章回答什么问题

- `remote/` 目录里到底有什么？
- `bridge/` 是做什么的？
- permission callback 为什么会进入 bridge？
- remote session 和本地会话是什么关系？

## 关键文件

- `restored-src/src/remote/RemoteSessionManager.ts`
- `restored-src/src/remote/SessionsWebSocket.ts`
- `restored-src/src/remote/remotePermissionBridge.ts`
- `restored-src/src/bridge/bridgeMain.ts`
- `restored-src/src/bridge/replBridge.ts`
- `restored-src/src/bridge/remoteBridgeCore.ts`

## 阅读入口

- 快速版：[`SIMPLE/README.md`](./SIMPLE/README.md)
- 深度版：[`DEEP/README.md`](./DEEP/README.md)
- Agent 入口：[`AI-AGENT/agent-readme.txt`](./AI-AGENT/agent-readme.txt)
- 轻量比较：[`comparison.md`](./comparison.md)

