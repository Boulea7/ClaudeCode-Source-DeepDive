# MODULES

这里是仓库的主内容，也是最适合按主题系统阅读的入口。

## 推荐顺序

1. `01-agent-loop-and-teams`
2. `03-persistent-memory-system`
3. `02-planning-compaction-and-assistant`
4. `05-tools-mcp-skills-and-plugins`
5. `06-permissions-sandbox-and-trust`
6. `04-buddy-voice-vim-and-terminal-ui`
7. `07-remote-session-bridge-and-sdk`
8. `08-prompts-config-and-other-moats`

## 按问题选择章节

### 想先看主循环和多 agent

- `01-agent-loop-and-teams`
- `02-planning-compaction-and-assistant`

### 想先看 memory / compact / 长会话

- `03-persistent-memory-system`
- `02-planning-compaction-and-assistant`

### 想先看扩展面

- `05-tools-mcp-skills-and-plugins`
- `06-permissions-sandbox-and-trust`

### 想先看远端与 bridge

- `07-remote-session-bridge-and-sdk`

### 想先看 prompt 和 feature gate

- `08-prompts-config-and-other-moats`
- `../PROMPTS/`
- `../FEATURE-FLAGS/`

## 阅读建议

- 第一次看：先读每章 `README.md`
- 想快速理解：读各章 `SIMPLE/README.md`
- 想跟源码：读各章 `DEEP/README.md`
- 想给 Agent 用：读各章 `AI-AGENT/agent-readme.txt`

## 章节定位

### `01-agent-loop-and-teams`

- 主线程、subagent、task list、fork / teammate 编排。

### `02-planning-compaction-and-assistant`

- Plan Mode、compact 路径、TodoWrite / Task V2 / runtime task 分层。

### `03-persistent-memory-system`

- `SessionMemory`、durable memory、team memory、daily-log / distilled index 边界。

### `04-buddy-voice-vim-and-terminal-ui`

- companion、vim 输入状态机、voice gating 与终端交互层。

### `05-tools-mcp-skills-and-plugins`

- tool contract、MCP 客户端链、skills 命令化、plugin 装配。

### `06-permissions-sandbox-and-trust`

- 权限规则、审批 UI、classifier、安全边界与 sandbox。

### `07-remote-session-bridge-and-sdk`

- `remote/` 现有 session attach 层、`bridge/` 本地出站桥接层、SDK 接线边界。

### `08-prompts-config-and-other-moats`

- system prompt sections、dynamic boundary、main-thread / subagent prompt 装配与若干 feature gate。
