[简体中文](./README.md) | [English](./README.en.md)

# 03 Persistent Memory System

This chapter explains how Claude Code splits its memory stack into session memory, durable personal memory, and team memory, then keeps those layers useful across long-running sessions.

In the public source mirror, those layers live in `services/SessionMemory/*`, `memdir/*` plus `services/extractMemories/*`, and `memdir/teamMemPaths.ts` plus `services/teamMemorySync/*`. `autoDream` adds a conditional background consolidation path. It belongs to the memory system, but it should not be described as an always-on product capability.

## What You Should Understand After This Chapter

- why `SessionMemory`, durable memory, and team memory need separate wording
- what `MEMORY.md` and topic files each do inside auto memory
- why team memory lives under the auto-memory tree rather than a separate root
- why `autoDream`, KAIROS daily-log mode, and `/dream` need conditional wording

## Key Files

- `_upstream/claude-code-sourcemap/restored-src/src/services/SessionMemory/sessionMemory.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/services/SessionMemory/sessionMemoryUtils.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/services/SessionMemory/prompts.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/services/extractMemories/extractMemories.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/memdir/memdir.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/memdir/memoryScan.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/memdir/teamMemPaths.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/services/teamMemorySync/index.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/services/teamMemorySync/watcher.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/services/autoDream/autoDream.ts`

## Where To Start

- quick guide: [SIMPLE/README.en.md](./SIMPLE/README.en.md)
- deep dive: [DEEP/README.en.md](./DEEP/README.en.md)
- short comparison: [comparison.en.md](./comparison.en.md)
