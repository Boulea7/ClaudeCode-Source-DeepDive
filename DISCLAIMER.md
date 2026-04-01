[简体中文](./DISCLAIMER.md) | [English](./DISCLAIMER.en.md)

# Disclaimer

## 仓库定位

这是一份面向开发者的非官方研究文档。

这里记录的是对公开镜像源码的阅读结果，目标是把运行链、模块边界和实现细节写得更清楚、更可复核。

## 代码事实边界

本仓库中的源码相关结论，只来自以下两处：

- `https://github.com/ChinaSiro/claude-code-sourcemap`
- 本地镜像：`_upstream/claude-code-sourcemap/`

如果某个判断无法回到这两处复核，本仓库不会把它写成源码事实。

## 这份仓库包含什么

- 架构总览
- 模块级源码走读
- prompt 装配机制说明
- tools、MCP、skills、plugins、permissions、memory、compact、tasks、remote 等运行链说明
- feature gate 与隐藏能力线索整理

## 这份仓库不包含什么

- 官方文档
- 官方发布说明
- 内部仓库还原
- 大段 raw prompt
- 无源码支撑的产品结论

## 需要保守描述的名称

下列名称即使在代码中出现，也只应按源码线索保守描述：

- `Buddy`
- `KAIROS`
- `PROACTIVE`
- `voice`
- `TEAMMEM`
- `CHICAGO_MCP`
- `bridge`
- `remote isolation`

推荐写法是：

- 有代码线索
- 当前镜像未完全坐实
- 不能过度下结论
- 不能确认公开发布状态

## 与官方的关系

本仓库与 Anthropic 无隶属关系，也不代表任何官方内部结构、产品命名或发布时间线。

这里的整理与评论，只代表对公开镜像的阅读结果。

## 引用建议

如果你要引用这里的内容，建议同时保留这三条：

1. 这是非官方研究文档
2. 源码事实以公开镜像和本地 `_upstream` 镜像为边界
3. feature gate 与隐藏分支不等于正式公开能力

## 写作规则

- 重要结论尽量挂回源码路径
- `PROMPTS/` 只解释装配机制，不贴大段 raw prompt
- `FEATURE-FLAGS/` 只写代码中的 gate 与分支，不写成发布说明
- 证据不足的地方优先缩小表述范围
