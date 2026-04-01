[简体中文](./agent-memory-compact-gates.md) | [English](./agent-memory-compact-gates.en.md)

# Agent, Memory, And Compact Gates

This page collects gates that affect agent spawning, memory behavior, compaction paths, and task-layer switching.

## What This Page Covers

- agent spawn / fork / teammate gates
- SessionMemory, memdir, and team-memory gates
- compaction and task/todo switching gates

## Main Points

- `FORK_SUBAGENT` changes the default spawn meaning when `subagent_type` is omitted
- SessionMemory and durable memory should stay separated in wording
- team memory stays under gated auto-memory paths
- KAIROS memory-related clues remain partial and should stay conservative
- Task V2 and TodoWrite switching is runtime strategy, not one generic task type

## Conservative Boundaries

- do not merge SessionMemory, durable memory, and team memory into one layer
- do not overstate `/dream`, nightly distillation, or KAIROS rollout
- do not flatten task layers into one “task system”
