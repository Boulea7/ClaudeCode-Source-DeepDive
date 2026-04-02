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
- `_upstream/claude-code-sourcemap/restored-src/src/services/mcp/client.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/services/mcp/auth.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/skills/loadSkillsDir.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/commands.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/SkillTool/SkillTool.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/plugins/loadPluginCommands.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/plugins/pluginLoader.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/main.tsx`

## Execution Flow

### 1. `Tool.ts` defines the shared contract first

`Tool.ts` is the protocol layer for the whole tool system. It defines the shared tool shape, the permission context, and the runtime context that later flows into tool execution.

That matters because Claude Code does not treat tools as plain callable names. A tool already carries runtime state, permission semantics, and rendering-related context before `query()` starts using it.

### 2. `tools.ts` separates candidate sets from the final runtime pool

The important distinction in `tools.ts` is not just “built-in versus MCP”. The file also separates:

- the broad built-in candidate set
- the built-in set that is visible in the current session
- the final built-in plus MCP pool used by runtime and prompt assembly
- a flat merged list that does not perform the final shaping step

`getTools()` applies filtering such as simple mode, deny rules, and `tool.isEnabled()` checks. `assembleToolPool()` then applies another layer by filtering MCP tools, sorting both sides, and deduplicating by tool name.

That is why `getMergedTools()` should not be described as the final runtime tool pool.

### 3. `MCPTool.ts` is only a template

The current mirror shows that actual MCP tools are instantiated in the MCP client path, not in `tools/MCPTool/MCPTool.ts` alone.

The MCP client flow does at least these steps:

1. choose a transport
2. connect the client
3. fetch `tools/list`
4. fetch `prompts/list`
5. fetch `resources/list`
6. convert those results into local `Tool`, `Command`, and `ServerResource` objects
7. handle reconnects, session expiry, 401s, and URL elicitation

This is also where server-specific naming behavior shows up. In the ordinary case, MCP tools are named like `mcp__<server>__<tool>`. Under a narrow SDK-related branch, an MCP tool can also shadow a built-in name directly.

### 4. Resources and auth pseudo-tools are host-side additions

MCP integration does not stop at remote `tools/list`.

The host can inject extra helpers:

- `ListMcpResourcesTool`
- `ReadMcpResourceTool`
- `mcp__<server>__authenticate`

These should stay described as host-side additions. They are not plain echoes of the remote server’s own tool list.

The current mirror also shows an important implementation detail in `ReadMcpResourceTool`: blob resources are written to disk first, then a saved path is returned. The normal path is not “inline a huge base64 blob into prompt context”.

### 5. Skills are produced as prompt commands before `SkillTool` executes them

`loadSkillsDir.ts` turns skill assets into `Command(type: 'prompt')` objects. `commands.ts` then assembles those command sets for different consumers. `SkillTool.ts` is the execution shell on top of that assembled command space.

That separation matters because discovery and execution are not the same phase:

- `loadSkillsDir.ts` handles discovery and command production
- `commands.ts` handles assembly and filtered views
- `SkillTool.ts` handles runtime execution

### 6. `SkillTool` execution is wider than the model-visible listing

One of the easiest mistakes in this area is to collapse “what the model sees” and “what runtime can execute” into a single skill list.

The current mirror supports a more conservative split:

- runtime execution can draw from a broader command set
- `getSkillToolCommands()` is closer to the model-facing listing
- `getMcpSkillCommands()` adds MCP-derived prompt-command supplements
- `attachments.ts` can expose a combined `skill_listing` attachment to the model

So `skill_listing` should stay described as a model-visible surface, not as the complete execution set.

### 7. Built-in plugin wiring exists, but the current mirror still looks like scaffold-level startup

`main.tsx` does wire `initBuiltinPlugins()` and `initBundledSkills()` during startup. But the current mirror still shows built-in plugin registration at scaffold level.

That is why the safer wording is:

- startup wiring exists
- registry and scaffold exist
- the current mirror does not yet show concrete built-in plugin registrations in active use

## Why This Layer Matters

This layer explains why Claude Code feels more like a composed runtime than a single “tool call” feature.

The architecture deliberately separates:

- tool contracts
- runtime tool-pool shaping
- remote MCP integration
- prompt-command production
- plugin packaging and startup wiring

That makes it possible for one capability to appear as a built-in tool, arrive dynamically from MCP, surface as a prompt command, or be bundled through plugin-related scaffolding.

## Conservative Boundaries

- keep `ListMcpResourcesTool`, `ReadMcpResourceTool`, and `mcp__<server>__authenticate` described as host-side additions
- keep `SkillTool` execution separate from the narrower `skill_listing` surface
- keep `CHICAGO_MCP` described as a gated computer-use branch, not as the MCP client’s general rollout state
- keep built-in plugins at registry/scaffold wording unless stronger source evidence is re-read

## Read Next

- [README.en.md](../README.en.md)
- [comparison.en.md](../comparison.en.md)
