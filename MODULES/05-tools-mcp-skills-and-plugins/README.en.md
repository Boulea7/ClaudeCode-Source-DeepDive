[简体中文](./README.md) | [English](./README.en.md)

# 05 Tools, MCP, Skills, And Plugins

This chapter explains how Claude Code splits its extensibility surface into separate layers.

## What You Should Understand After This Chapter

- how local tools and MCP tools enter the same runtime
- why resources are handled separately
- what skills and plugins each contribute
- why `services/mcp/` takes on so much responsibility

## Key Files

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

## Where To Start

- quick guide: [SIMPLE/README.en.md](./SIMPLE/README.en.md)
- deep dive: [DEEP/README.en.md](./DEEP/README.en.md)
- short comparison: [comparison.en.md](./comparison.en.md)
