# 08 Prompts, Config, And Other Moats

这一章用来收纳几个前面各章都会碰到、但单独拿出来更容易讲清楚的系统。

它更像一本“补全说明书”：把 prompt 装配、config 影响面和若干容易散落的关键机制单独讲清楚。

## 读完这一章，你会更清楚什么

- system prompt 是怎么装配的？
- config 为什么会影响很多运行时行为？
- 还有哪些不容易被归进前面模块，但很关键的设计点？

## 关键文件

- `restored-src/src/constants/prompts.ts`
- `restored-src/src/utils/systemPrompt.ts`
- `restored-src/src/constants/systemPromptSections.ts`
- `restored-src/src/main.tsx`
- `restored-src/src/bootstrap/`

## 从哪里开始读

- 快速版：[`SIMPLE/README.md`](./SIMPLE/README.md)
- 深度版：[`DEEP/README.md`](./DEEP/README.md)
- Agent 入口：[`AI-AGENT/agent-readme.txt`](./AI-AGENT/agent-readme.txt)
- 轻量比较：[`comparison.md`](./comparison.md)
