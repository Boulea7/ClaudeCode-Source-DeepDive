[简体中文](./README.md) | [English](./README.en.md)

# Tools, MCP, Skills, And Plugins In One Minute

Keep one line in mind first:

tools, resources, skills, and plugins are not the same layer.

```mermaid
flowchart TD
    A[Built-in Tools] --> E[Tool Runtime]
    B[MCP Tools] --> E
    C[MCP Resources] --> F[Context Layer]
    D[Skills / Plugins] --> G[Prompt And Capability Layer]
    E --> H[QueryEngine]
    F --> H
    G --> H
```

## Three Takeaways

- tools and resources belong to different layers
- MCP affects both tool execution and context access
- skills and plugins serve different roles

## Read Next

- overview: [README.en.md](../README.en.md)
- deep dive: [DEEP/README.en.md](../DEEP/README.en.md)
