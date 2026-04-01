# 1 分钟看懂 Prompts, Config, And Other Moats

先用一张图看：

这一章更像一本“补全说明书”，把前面几章经常会碰到、但不适合散着讲的东西集中说明。

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

## 下一步去哪里

- 想先看整体：读 `README.md`
- 想继续看 prompt 装配：读 `DEEP/README.md`
