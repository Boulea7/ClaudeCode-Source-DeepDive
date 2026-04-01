# 06 Permissions, Sandbox, And Trust

这一章解释 Claude Code 为什么不是“默认可以做一切”的 agent。

如果你想先弄清楚“为什么它不是一个毫无边界的命令执行器”，可以直接读这一章。

## 读完这一章，你会更清楚什么

- permission mode 是怎么工作的？
- 规则、审批、UI、sandbox 是怎么连接起来的？
- 为什么同意一次和长期规则不是一回事？
- `auto mode`、classifier、dangerous pattern 在哪里出现？

## 关键文件

- `restored-src/src/utils/permissions/`
- `restored-src/src/components/permissions/`
- `restored-src/src/services/mcpServerApproval.tsx`
- `restored-src/src/services/tools/toolExecution.ts`

## 从哪里开始读

- 快速版：[`SIMPLE/README.md`](./SIMPLE/README.md)
- 深度版：[`DEEP/README.md`](./DEEP/README.md)
- Agent 入口：[`AI-AGENT/agent-readme.txt`](./AI-AGENT/agent-readme.txt)
- 轻量比较：[`comparison.md`](./comparison.md)
