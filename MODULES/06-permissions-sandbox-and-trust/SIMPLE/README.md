[简体中文](./README.md) | [English](./README.en.md)

# 1 分钟看懂 Permissions, Sandbox, And Trust

先看最短的流程：

```mermaid
flowchart TD
    A[Tool Call] --> B[Permission Rules]
    B --> C[allow / deny / ask]
    C --> D[Permission UI]
    C --> E[Sandbox Layer]
    D --> F[Final Decision]
    E --> F
```

## 三个要点

- permission rules 决定是否需要询问
- 审批 UI 决定用户如何回答
- sandbox 决定放行之后的运行范围

## 下一步去哪里

- 总览：[README.md](../README.md)
- 深读：[DEEP/README.md](../DEEP/README.md)
