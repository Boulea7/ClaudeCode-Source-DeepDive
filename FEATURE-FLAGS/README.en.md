[简体中文](./README.md) | [English](./README.en.md)

# FEATURE-FLAGS

This document set tracks the gates that reshape runtime paths, prompt paths, memory paths, and remote paths.

## Reading Order

1. [runtime-and-prompt-gates.en.md](./runtime-and-prompt-gates.en.md)
2. [agent-memory-compact-gates.en.md](./agent-memory-compact-gates.en.md)
3. [remote-bridge-and-session-gates.en.md](./remote-bridge-and-session-gates.en.md)

## Boundary Notes

- `feature()` marks compile-time gates.
- GrowthBook and env switches mark runtime gates.
- A gate in code proves a branch exists. It does not prove rollout.
- A name in code does not prove a public product name.
- `Buddy`, `KAIROS`, `PROACTIVE`, `voice`, `bridge`, and `remote` stay under conservative wording.

## Main Source Spine Re-read In This Pass

- `_upstream/claude-code-sourcemap/restored-src/src/constants/prompts.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/screens/REPL.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/QueryEngine.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/AgentTool.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/forkSubagent.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/services/SessionMemory/sessionMemory.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/memdir/memdir.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/memdir/paths.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/memdir/teamMemPaths.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/services/compact/autoCompact.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/tasks.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/bridge/bridgeEnabled.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/bridge/initReplBridge.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/bridge/bridgeMain.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/entrypoints/agentSdkTypes.ts`
