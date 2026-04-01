[简体中文](./README.md) | [English](./README.en.md)

# FEATURE-FLAGS

这一组文档把源码里会改写运行路径的 gate 和隐藏分支单独整理出来。

## 这组文档关注什么

- `feature()` 这类编译期 gate
- GrowthBook、env 等运行时 gate
- prompt、memory、agent、remote、bridge、voice、companion 等条件分支

## 建议阅读顺序

1. [runtime-and-prompt-gates.md](./runtime-and-prompt-gates.md)
2. [agent-memory-compact-gates.md](./agent-memory-compact-gates.md)
3. [remote-bridge-and-session-gates.md](./remote-bridge-and-session-gates.md)

## 写法边界

- 代码里出现 gate，不等于公开 rollout
- 代码里出现名称，不等于公开产品命名
- 编译期 gate 和运行时 gate 要分开写
- `Buddy`、`KAIROS`、`PROACTIVE`、`voice`、`bridge`、`remote isolation` 等名称都要保守描述
