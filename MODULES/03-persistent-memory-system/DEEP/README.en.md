[简体中文](./README.md) | [English](./README.en.md)

# Deep Dive: Persistent Memory System

This chapter separates four memory-related runtime paths: entrypoint injection, session summaries, durable writes, and query-time recall.

## What This Chapter Covers

- where memory files enter context
- how `SessionMemory` serves conversation continuity
- how durable memory files are written and recalled
- where team memory sits in the memory tree

## Key Source Files

- `_upstream/claude-code-sourcemap/restored-src/src/utils/claudemd.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/services/SessionMemory/`
- `_upstream/claude-code-sourcemap/restored-src/src/services/extractMemories/`
- `_upstream/claude-code-sourcemap/restored-src/src/memdir/`

## Main Points

- `claudemd` controls entrypoint-style instruction and memory-file injection.
- `SessionMemory` maintains `summary.md` for the current session.
- `extractMemories` writes durable memory topic files.
- `findRelevantMemories()` surfaces topic files during recall.
- team memory lives under the auto-memory tree rather than as a separate root.

## Conservative Boundaries

- KAIROS daily-log, `/dream`, team-memory sync, and related flows should remain narrower unless they are re-read directly for this page.
- exact path formulas should be tied to the filesystem helpers that define them.
- `SessionMemory`, durable memory, and team memory should stay separated in wording.

## Read Next

- [README.en.md](../README.en.md)
- [comparison.en.md](../comparison.en.md)
