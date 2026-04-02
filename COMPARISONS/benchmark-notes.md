[简体中文](./benchmark-notes.md) | [English](./benchmark-notes.en.md)

# Benchmark Notes

公开 benchmark 可以提供参考，但不能代替源码分析。

如果你想理解 Claude Code 为什么会被频繁比较，这页已经够用。想理解它到底怎么实现，还是应该回到源码章节。

## 可以得出的结论

- 模型 benchmark 能说明模型能力趋势
- 产品 benchmark 往往受 scaffold、权限、预算、工具接入方式影响很大
- 很难找到一个完全公正的公开 benchmark，直接裁决 `Claude Code vs Cursor vs Codex CLI vs Aider`

## 这对本仓库意味着什么

- benchmark 只用来补背景
- 源码拆解才是主内容
- 如果 benchmark 和源码结构之间有关系，这里只解释可能原因

## 边界

- benchmark 不是产品优劣裁决器
- benchmark 不能替代源码结构分析
- benchmark 结果也不能直接证明运行时设计细节

## 来源

- Anthropic `Claude 3.7 Sonnet and Claude Code`
- OpenAI `Introducing Codex`
- OpenAI `Introducing upgrades to Codex`
- CursorBench 说明
- Aider benchmarks

## 返回阅读路径

- [COMPARISONS/README.md](./README.md)
- [README.md](../README.md)
