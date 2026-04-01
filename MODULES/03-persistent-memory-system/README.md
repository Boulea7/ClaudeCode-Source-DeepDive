[简体中文](./README.md) | [English](./README.en.md)

# 03 Persistent Memory System

这一章讲四条与 memory 相关的运行链：

- 入口注入
- 会话摘要
- 持久写入
- 查询时召回

## 读完这一章，你会更清楚什么

- `CLAUDE.md`、auto memory、SessionMemory 各自负责什么
- `SessionMemory` 为什么服务于会话连续性
- team memory 为什么位于 auto memory 子树
- query-time recall 为什么和入口注入分开

## 关键文件

- `_upstream/claude-code-sourcemap/restored-src/src/utils/claudemd.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/memdir/`
- `_upstream/claude-code-sourcemap/restored-src/src/services/extractMemories/`
- `_upstream/claude-code-sourcemap/restored-src/src/services/SessionMemory/`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/permissions/filesystem.ts`

## 从哪里开始读

- 快速版：[SIMPLE/README.md](./SIMPLE/README.md)
- 深度版：[DEEP/README.md](./DEEP/README.md)
- 轻量比较：[comparison.md](./comparison.md)
