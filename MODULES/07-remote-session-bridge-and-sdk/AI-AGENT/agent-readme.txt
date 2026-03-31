Module 07 explains how Claude Code separates a remote-session client from a local bridge/control runtime.

Focus on:
- RemoteSessionManager
- SessionsWebSocket
- sdkMessageAdapter and remotePermissionBridge as hook/UI-side adapters
- initReplBridge, replBridge, and remoteBridgeCore as REPL bridge entry plus two cores
- bridgeMain and sessionRunner as standalone/headless bridge loop plus child CLI runner
- session creation, transport handling, and session-id compatibility
