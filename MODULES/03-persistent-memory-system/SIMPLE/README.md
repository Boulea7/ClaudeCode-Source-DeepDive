[简体中文](./README.md) | [English](./README.en.md)

# 1 分钟看懂 Persistent Memory System

先把 Claude Code 的 memory 看成几条并行链：

```mermaid
flowchart TD
    A[claudemd entrypoints] --> B[user context injection]
    C[SessionMemory] --> D[session-memory/summary.md]
    D --> E[sessionMemoryCompact]
    F[extractMemories] --> G[auto memory root]
    G --> H[topic files]
    I[findRelevantMemories(memoryDir)] --> J[relevant-memory attachments]
```

## 三个要点

- `claudemd` 负责入口注入
- `SessionMemory` 维护会话摘要
- `extractMemories + memdir` 负责 durable memory 写入与召回规则

## 下一步去哪里

- 总览：[README.md](../README.md)
- 深读：[DEEP/README.md](../DEEP/README.md)
