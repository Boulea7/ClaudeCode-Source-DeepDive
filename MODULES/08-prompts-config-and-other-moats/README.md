[简体中文](./README.md) | [English](./README.en.md)

# 08 Prompts, Config, And Runtime Glue

这一章集中说明 prompt 装配、config 影响面和若干容易散落的关键机制。

## 读完这一章，你会更清楚什么

- system prompt 如何装配
- config 如何影响运行时行为
- `dynamic boundary` 为什么要按条件理解
- 哪些启动阶段的决定会持续影响后面的会话

## 关键文件

- `_upstream/claude-code-sourcemap/restored-src/src/constants/prompts.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/constants/systemPromptSections.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/systemPrompt.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/queryContext.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/screens/REPL.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/QueryEngine.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/main.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/bootstrap/`

## 从哪里开始读

- 快速版：[SIMPLE/README.md](./SIMPLE/README.md)
- 深度版：[DEEP/README.md](./DEEP/README.md)
- 轻量比较：[comparison.md](./comparison.md)
