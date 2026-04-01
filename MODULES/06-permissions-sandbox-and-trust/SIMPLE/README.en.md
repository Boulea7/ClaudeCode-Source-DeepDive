[简体中文](./README.md) | [English](./README.en.md)

# Permissions, Sandbox, And Trust In One Minute

Start with the shortest flow:

```mermaid
flowchart TD
    A[Tool Call] --> B[Permission Rules]
    B --> C[allow / deny / ask]
    C --> D[Permission UI]
    C --> E[Sandbox Layer]
    D --> F[Final Decision]
    E --> F
```

## Three Takeaways

- permission rules decide whether the tool call needs asking
- approval UI decides how the user answers
- sandboxing decides what the runtime can still do after approval

## Read Next

- overview: [README.en.md](../README.en.md)
- deep dive: [DEEP/README.en.md](../DEEP/README.en.md)
