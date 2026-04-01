[简体中文](./README.md) | [English](./README.en.md)

# Deep Dive: Tools, MCP, Skills, And Plugins

This chapter explains how Claude Code splits tool execution, MCP integration, skill commands, and plugin loading into separate layers.

## What This Chapter Covers

- the shared tool contract and tool pool
- the MCP client path for tools, commands, and resources
- skill command production and execution
- plugin loading and startup wiring

## Key Source Files

- `_upstream/claude-code-sourcemap/restored-src/src/Tool.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/services/mcp/`
- `_upstream/claude-code-sourcemap/restored-src/src/skills/`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/SkillTool/`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/plugins/`
- `_upstream/claude-code-sourcemap/restored-src/src/main.tsx`

## Main Points

- `Tool.ts` defines the shared tool contract.
- `tools.ts` controls built-in tools, MCP tool assembly, and final pool shaping.
- MCP resources and auth pseudo-tools are host-side additions, not plain `tools/list` echoes.
- skills are first produced as `Command(type: 'prompt')` objects.
- `SkillTool` executes commands; it does not discover them.
- built-in plugin startup wiring exists, but the current mirror still shows scaffold-level registration.

## Conservative Boundaries

- keep `processPromptSlashCommand()` limited to local/plugin/MCP prompt-command expansion
- keep `skill_listing` separate from the broader execution set
- keep `CHICAGO_MCP` as a gated computer-use branch, not a general MCP rollout claim

## Read Next

- [README.en.md](../README.en.md)
- [comparison.en.md](../comparison.en.md)
