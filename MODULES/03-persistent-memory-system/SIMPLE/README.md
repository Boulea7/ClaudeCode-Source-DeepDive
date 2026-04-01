# 1 分钟看懂 Persistent Memory System

先把 Claude Code 的 memory 想成几条并行链：

如果你最关心“它为什么像是能持续记住东西”，先记住这页的分层通常就够了。

```mermaid
flowchart TD
    A[claudemd entrypoints] --> B[user context injection]
    C[SessionMemory] --> D[session-memory/summary.md]
    D --> E[sessionMemoryCompact]
    F[extractMemories] --> G[auto memory root]
    G --> H[topic files]
    I[findRelevantMemories(memoryDir)] --> J[relevant-memory attachments]
```

## 几条链分别是什么

- `claudemd` 入口文件：负责把指令文件与 memory 入口文件拼进 user context
- `SessionMemory`：维护当前会话的 `summary.md`
- `extractMemories + memdir`：负责 durable memory 的写入与目录规则
- `findRelevantMemories()`：按调用方传入目录挑选相关 topic files

## 为什么重要

这不是“多放几个笔记文件”，而是几条在不同阶段参与运行时的上下文机制。

## 下一步去哪里

- 想先建立整体感觉：回到 `README.md`
- 想真正搞清边界：读 `DEEP/README.md`
