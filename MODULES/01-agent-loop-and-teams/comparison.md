[简体中文](./comparison.md) | [English](./comparison.en.md)

# 轻量比较

很多工具支持并行 worker 或多任务执行。

Claude Code 在这一层的区别点更具体：

- 交互式会话与无头会话共享同一套 `query()` 回合循环
- 子 agent 调度走正式工具路径，不是纯 prompt 约定
- 后台任务、远端任务、shell 和 teammate 共享任务表示层
- 主会话后台化仍然落在这套任务框架里
