[简体中文](./README.md) | [English](./README.en.md)

# 01 Agent Loop And Teams

This chapter focuses on the part of Claude Code that looks most like a runtime system.

Start here if you want to understand how the main thread, workers, tasks, and team features connect to the same execution chain.

## What You Should Understand After This Chapter

- how the main thread and workers divide responsibilities
- where `AgentTool` sits in the orchestration chain
- how tasks, teams, and teammates enter the same state layer
- why fork subagents need to be treated separately

## Key Files

- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/AgentTool.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/runAgent.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/forkSubagent.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/loadAgentsDir.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tasks/`
- `_upstream/claude-code-sourcemap/restored-src/src/coordinator/coordinatorMode.ts`

## Where To Start

- quick guide: [SIMPLE/README.en.md](./SIMPLE/README.en.md)
- deep dive: [DEEP/README.en.md](./DEEP/README.en.md)
- short comparison: [comparison.en.md](./comparison.en.md)
