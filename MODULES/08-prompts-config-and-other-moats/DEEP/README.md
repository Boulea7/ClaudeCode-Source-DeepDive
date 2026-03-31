# 深度拆解：Prompts, Config, And Other Moats

这一章适合在你已经看过 `QueryEngine`、memory、tools 之后再读。

## 为什么这章重要

很多系统行为之所以成立，不只是因为某个模块本身，而是因为：

- 启动阶段先做了准备
- system prompt 被按模式重组
- config 和 feature flag 改变了运行路径

## 关键阅读线

### 1. 从 `main.tsx` 开始

`restored-src/src/main.tsx` 很大，但它非常值。  
它会告诉你 Claude Code 在真正进入主循环前，已经做了哪些准备。

### 2. 看 `systemPrompt.ts`

`restored-src/src/utils/systemPrompt.ts` 很关键，因为它说明了 prompt 的优先级和组合方式。

### 3. 再看 `prompts.ts` 和 `systemPromptSections.ts`

这两部分一起看，能理解：

- 默认 prompt 来自哪里
- section 是怎么组织的
- 为什么 prompt 可以被局部替换或重建

## 这一章最值得记住的一句话

Claude Code 的很多“体验差异”并不是某个单功能带来的，而是启动、配置、prompt 组织方式一起决定的。

