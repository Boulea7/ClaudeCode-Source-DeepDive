[简体中文](./exposure-surfaces-and-risks.md) | [English](./exposure-surfaces-and-risks.en.md)

# 可见面、暴露面与保守边界

这一页解释 prompt 相关文档里最容易写过头的几个地方。

## 这里关注什么

- 哪些内容可以讲机制
- 哪些内容只能做来源索引
- 哪些名字只能保守写成 gated branch
- 哪些 attachment 会进入模型可见面

## 可以讲清机制的面

- `default prompt parts`
- `dynamic sections`
- `SYSTEM_PROMPT_DYNAMIC_BOUNDARY`
- interactive / non-interactive 主线程 prompt 路径
- ordinary subagent / fork subagent prompt 路径
- `skill_listing` 与 `command_permissions` attachment

## 只做来源索引更稳妥的面

- 大段 raw system prompt
- 大段 raw agent prompt
- 大段 skill body
- 未完整坐实的内部 helper 与内部 rollout 语义

## 高风险误写点

- 把 `SYSTEM_PROMPT_DYNAMIC_BOUNDARY` 写成每次都会出现的固定段落
- 把 `mcp_instructions` 写成唯一固定的内联 section
- 把 fork 写成和父线程完全等同
- 把 `Buddy`、`KAIROS`、`PROACTIVE` 写成公开固定模式

## 这组文档的保守边界

- 只解释装配机制
- 不转储整份 raw prompt
- feature gate 只说明代码分支
- rollout 状态必须继续保守
