[简体中文](./README.md) | [English](./README.en.md)

# Planning, Compaction, And Assistant In One Minute

This chapter makes more sense if you split it into parallel mechanisms:

```mermaid
flowchart TD
    A[EnterPlanModeTool] --> B[toolPermissionContext.mode = plan]
    B --> C[read-only planning state]
    D[attachments / plan prompts] --> E[plan file create or edit]
    F[autoCompactIfNeeded] --> G[trySessionMemoryCompaction]
    G -->|fallback| H[compactConversation]
    I[TodoWrite v1] --> J[AppState.todos]
    K[Task V2] --> L[task-list files]
    M[runtime task] --> N[AppState.tasks + output files]
```

## Three Takeaways

- `Plan Mode` combines permission state and follow-up prompt attachments
- the plan file is a separate artifact
- `TodoWrite`, Task V2, and runtime tasks are three different layers

## Read Next

- overview: [README.en.md](../README.en.md)
- deep dive: [DEEP/README.en.md](../DEEP/README.en.md)
