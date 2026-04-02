[简体中文](./README.md) | [English](./README.en.md)

# 01 Agent Loop And Teams

This chapter explains how Claude Code places the main session, child agents, background tasks, and team-style coordination inside one runtime.

In the public source mirror, that chain sits in `main.tsx`, `screens/REPL.tsx`, `QueryEngine.ts`, `query.ts`, `tools/AgentTool/*`, and `tasks/*`. The interactive entry path and the headless entry path share the same `query()` turn loop. `AgentTool` selects the child-agent path. `runAgent()` executes the child session. `tasks/*` gives local agents, remote agents, backgrounded main sessions, shell work, and in-process teammates a common task-state layer.

## What You Should Understand After This Chapter

- how `main.tsx -> REPL.tsx -> query.ts` differs from `main.tsx -> QueryEngine.ts -> query.ts`
- what `AgentTool`, `runAgent()`, and `forkSubagent.ts` each own
- why fork workers and ordinary subagents need different inheritance wording
- how `local_agent`, `remote_agent`, `in_process_teammate`, and `main-session` fit into task state

## Key Files

- `_upstream/claude-code-sourcemap/restored-src/src/main.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/screens/REPL.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/QueryEngine.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/query.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/AgentTool.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/runAgent.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/forkSubagent.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/resumeAgent.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tasks/`

## Where To Start

- quick guide: [SIMPLE/README.en.md](./SIMPLE/README.en.md)
- deep dive: [DEEP/README.en.md](./DEEP/README.en.md)
- short comparison: [comparison.en.md](./comparison.en.md)
