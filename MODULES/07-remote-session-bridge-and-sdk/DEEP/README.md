# 深度拆解：Remote Session, Bridge, And SDK

这一章最值得注意的不是某一个函数，而是目录规模。

## 为什么 `bridge/` 值得重视

`restored-src/src/bridge/` 目录里可以直接看到很多重量级文件：

- `bridgeMain.ts`
- `bridgeMessaging.ts`
- `bridgeUI.ts`
- `remoteBridgeCore.ts`
- `replBridge.ts`
- `replBridgeTransport.ts`
- `sessionRunner.ts`
- `createSession.ts`
- `bridgePermissionCallbacks.ts`

这说明 bridge 不是一个“小桥接脚本”，而是一整层运行时。

## `remote/` 说明什么

`restored-src/src/remote/` 目录可直接看到：

- `RemoteSessionManager.ts`
- `SessionsWebSocket.ts`
- `remotePermissionBridge.ts`
- `sdkMessageAdapter.ts`

这至少说明：

- remote session 是真实存在的
- WebSocket 和 permission bridge 都是明确对象
- SDK message adapter 是这层系统的一部分

## 建议阅读顺序

1. `restored-src/src/remote/RemoteSessionManager.ts`
2. `restored-src/src/remote/remotePermissionBridge.ts`
3. `restored-src/src/bridge/bridgeMain.ts`
4. `restored-src/src/bridge/replBridge.ts`
5. `restored-src/src/bridge/remoteBridgeCore.ts`

## 这一章最值得记住的一句话

Claude Code 的会话系统并不只围绕一个本地 REPL，而是在向“可桥接、可远程、可切换的运行时”发展。

