[简体中文](./README.md) | [English](./README.en.md)

# 06 Permissions, Sandbox, And Trust

这一章解释 Claude Code 如何建立工具调用的信任边界。

## 读完这一章，你会更清楚什么

- permission mode 如何工作
- 规则、审批、UI、sandbox 如何接起来
- 单次同意和长期规则有什么区别
- `auto mode`、classifier、dangerous pattern 在哪里出现

## 关键文件

- `_upstream/claude-code-sourcemap/restored-src/src/utils/permissions/`
- `_upstream/claude-code-sourcemap/restored-src/src/components/permissions/`
- `_upstream/claude-code-sourcemap/restored-src/src/services/mcpServerApproval.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/services/tools/toolExecution.ts`

## 从哪里开始读

- 快速版：[SIMPLE/README.md](./SIMPLE/README.md)
- 深度版：[DEEP/README.md](./DEEP/README.md)
- 轻量比较：[comparison.md](./comparison.md)
