# 03 Persistent Memory System

这一章是本仓库最重要的模块之一。

Claude Code 的 memory 不是一个单文件功能，而是一条持久上下文链。

## 这一章回答什么问题

- `CLAUDE.md` 和 AutoMem 是什么关系？
- Session Memory 为什么不是普通笔记？
- Team Memory 为什么值得单独看？
- `compact` 为什么和 memory 紧密耦合？

## 关键文件

- `restored-src/src/utils/claudemd.ts`
- `restored-src/src/utils/config.ts`
- `restored-src/src/memdir/`
- `restored-src/src/services/extractMemories/`
- `restored-src/src/services/SessionMemory/`
- `restored-src/src/services/teamMemorySync/`

## 阅读入口

- 快速版：[`SIMPLE/README.md`](./SIMPLE/README.md)
- 深度版：[`DEEP/README.md`](./DEEP/README.md)
- Agent 入口：[`AI-AGENT/agent-readme.txt`](./AI-AGENT/agent-readme.txt)
- 轻量比较：[`comparison.md`](./comparison.md)

