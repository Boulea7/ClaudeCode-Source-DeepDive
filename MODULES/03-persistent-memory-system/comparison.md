# 轻量比较

很多工具也支持规则文件、历史记录、或者长上下文。

Claude Code 这一章更特别的地方是：它把下面这些对象做成了几条并行机制：

- `claudemd` 入口文件注入
- SessionMemory 会话摘要
- auto memory / team memory 持久文件
- query-time relevant-memory surfacing

这也是为什么它的 memory 体验更像几条并行机制，而不是一个单一记忆总线。
