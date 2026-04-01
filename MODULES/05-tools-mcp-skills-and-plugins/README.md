[简体中文](./README.md) | [English](./README.en.md)

# 05 Tools, MCP, Skills, And Plugins

这一章解释 Claude Code 的扩展面如何分层。

## 读完这一章，你会更清楚什么

- 本地工具和 MCP 工具如何进入同一套运行时
- resources 为什么要单独处理
- skills 和 plugins 分别承担什么角色
- `services/mcp/` 为什么会承担这么多工作

## 关键文件

- `_upstream/claude-code-sourcemap/restored-src/src/Tool.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/MCPTool/`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/ListMcpResourcesTool/`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/ReadMcpResourceTool/`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/SkillTool/`
- `_upstream/claude-code-sourcemap/restored-src/src/services/mcp/`
- `_upstream/claude-code-sourcemap/restored-src/src/skills/`
- `_upstream/claude-code-sourcemap/restored-src/src/plugins/`
- `_upstream/claude-code-sourcemap/restored-src/src/main.tsx`

## 从哪里开始读

- 快速版：[SIMPLE/README.md](./SIMPLE/README.md)
- 深度版：[DEEP/README.md](./DEEP/README.md)
- 轻量比较：[comparison.md](./comparison.md)
