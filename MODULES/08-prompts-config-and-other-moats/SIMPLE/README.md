# 1 分钟看懂 Prompts, Config, And Other Moats

先用一张图看：

```mermaid
flowchart TD
    A[main.tsx] --> B[bootstrap / config]
    B --> C[system prompt assembly]
    C --> D[QueryEngine]
    B --> E[feature flags / mode switches]
```

## 核心理解

- prompt 不是硬编码常量
- config 不只是读几个选项
- 启动阶段已经决定了很多后面的运行行为

