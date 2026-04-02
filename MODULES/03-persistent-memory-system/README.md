[简体中文](./README.md) | [English](./README.en.md)

# 03 Persistent Memory System

本章说明 Claude Code 的记忆层如何分成会话记忆、持久个人记忆、团队记忆三部分，并在长会话里继续生效。

公开镜像里，这三部分分别落在 `services/SessionMemory/*`、`memdir/*` 与 `services/extractMemories/*`、`memdir/teamMemPaths.ts` 与 `services/teamMemorySync/*`。`autoDream` 还提供了一条条件化的后台整理路径。它属于记忆系统的延伸机制，不应被写成固定开启的产品能力。

## 读完这一章，你会更清楚什么

- `SessionMemory`、durable memory、team memory 为什么必须分开写
- `MEMORY.md` 与 topic files 在 auto memory 里分别承担什么职责
- team memory 为什么位于 auto memory 子树，而不是独立根目录
- `autoDream`、KAIROS daily-log、`/dream` 为什么要保留条件化表述

## 关键文件

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

## 从哪里开始读

- 快速版：[SIMPLE/README.md](./SIMPLE/README.md)
- 深度版：[DEEP/README.md](./DEEP/README.md)
- 轻量比较：[comparison.md](./comparison.md)
