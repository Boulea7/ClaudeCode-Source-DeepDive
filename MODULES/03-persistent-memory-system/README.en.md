[简体中文](./README.md) | [English](./README.en.md)

# 03 Persistent Memory System

This chapter covers four memory-related runtime paths:

- entrypoint injection
- session summaries
- durable writes
- query-time recall

## What You Should Understand After This Chapter

- what `CLAUDE.md`, auto memory, and SessionMemory each do
- why `SessionMemory` serves conversation continuity
- why team memory lives under the auto-memory tree
- why query-time recall is separate from entrypoint injection

## Key Files

- `_upstream/claude-code-sourcemap/restored-src/src/utils/claudemd.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/memdir/`
- `_upstream/claude-code-sourcemap/restored-src/src/services/extractMemories/`
- `_upstream/claude-code-sourcemap/restored-src/src/services/SessionMemory/`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/permissions/filesystem.ts`

## Where To Start

- quick guide: [SIMPLE/README.en.md](./SIMPLE/README.en.md)
- deep dive: [DEEP/README.en.md](./DEEP/README.en.md)
- short comparison: [comparison.en.md](./comparison.en.md)
