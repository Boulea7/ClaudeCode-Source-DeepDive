[简体中文](./comparison.md) | [English](./comparison.en.md)

# 轻量比较

很多 AI coding 工具重点落在编辑器表面。

Claude Code 在这一层的区别点更清楚：

- 终端里有 companion surface
- voice 已经接入输入侧录音与 STT 链
- vim 模态输入有独立状态机与执行层
- 这些交互能力都接回 `REPL.tsx` 与 `PromptInput.tsx`
