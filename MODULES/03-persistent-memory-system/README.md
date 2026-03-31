# 03 Persistent Memory System

这一章是本仓库最重要的模块之一。

Claude Code 的 memory 不是一个单文件功能，而是几条并行的 persistence / recall 机制。

## 这一章回答什么问题

- `CLAUDE.md`、auto memory、SessionMemory 分别负责什么？
- Session Memory 为什么不是普通笔记？
- team memory 为什么是 auto memory 的子树？
- relevant memory recall 为什么不等于入口文件注入？

## 关键文件

- `restored-src/src/utils/claudemd.ts`
- `restored-src/src/memdir/`
- `restored-src/src/services/extractMemories/`
- `restored-src/src/services/SessionMemory/`
- `restored-src/src/utils/permissions/filesystem.ts`

## 阅读入口

- 快速版：[`SIMPLE/README.md`](./SIMPLE/README.md)
- 深度版：[`DEEP/README.md`](./DEEP/README.md)
- Agent 入口：[`AI-AGENT/agent-readme.txt`](./AI-AGENT/agent-readme.txt)
- 轻量比较：[`comparison.md`](./comparison.md)
