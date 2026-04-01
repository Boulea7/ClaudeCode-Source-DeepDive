[简体中文](./README.md) | [English](./README.en.md)

# Persistent Memory System In One Minute

Treat Claude Code memory as several parallel paths:

```mermaid
flowchart TD
    A[claudemd entrypoints] --> B[user context injection]
    C[SessionMemory] --> D[session-memory/summary.md]
    D --> E[sessionMemoryCompact]
    F[extractMemories] --> G[auto memory root]
    G --> H[topic files]
    I[findRelevantMemories(memoryDir)] --> J[relevant-memory attachments]
```

## Three Takeaways

- `claudemd` handles entrypoint injection
- `SessionMemory` maintains the session summary
- `extractMemories + memdir` handle durable memory writes and recall rules

## Read Next

- overview: [README.en.md](../README.en.md)
- deep dive: [DEEP/README.en.md](../DEEP/README.en.md)
