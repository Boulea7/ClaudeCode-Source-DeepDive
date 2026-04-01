# 03 Persistent Memory System

这一章是本仓库最重要的模块之一。

Claude Code 的 memory 不是一个单文件功能，而是几条并行的记忆写入与召回链。

如果你最关心“它为什么像是能连续记住东西”，通常应该优先读这一章。

## 读完这一章，你会更清楚什么

- `CLAUDE.md`、auto memory、SessionMemory 分别负责什么？
- Session Memory 为什么不是普通笔记？
- team memory 为什么是 auto memory 的子树？
- 相关记忆召回为什么不等于入口文件注入？

## 关键文件

- `restored-src/src/utils/claudemd.ts`
- `restored-src/src/memdir/`
- `restored-src/src/services/extractMemories/`
- `restored-src/src/services/SessionMemory/`
- `restored-src/src/utils/permissions/filesystem.ts`

## 从哪里开始读

- 快速版：[`SIMPLE/README.md`](./SIMPLE/README.md)
- 深度版：[`DEEP/README.md`](./DEEP/README.md)
- Agent 入口：[`AI-AGENT/agent-readme.txt`](./AI-AGENT/agent-readme.txt)
- 轻量比较：[`comparison.md`](./comparison.md)
