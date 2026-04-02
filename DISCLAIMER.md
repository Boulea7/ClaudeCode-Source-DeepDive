[简体中文](./DISCLAIMER.md) | [English](./DISCLAIMER.en.md)

# 仓库声明

## 仓库定位

这组文档服务于公开镜像源码阅读，主题集中在运行链、模块边界、工具系统、prompt 装配与条件路径。

Anthropic 官方结构、发布时间、产品命名、内部仓库内容超出这组文档的事实边界。

## 源码事实边界

本仓库中的源码相关结论只来自以下两处：

- `https://github.com/ChinaSiro/claude-code-sourcemap`
- 本地镜像：`_upstream/claude-code-sourcemap/`

如果某个判断无法回到这两处复核，这个仓库会把它写成阅读推断、线索或待确认点。

## 这组文档包含什么

- 架构总览
- 模块级源码走读
- prompt 装配机制说明
- tools、MCP、skills、plugins、permissions、memory、compact、tasks、remote 等运行链说明
- feature gate 与条件分支线索整理

## 这组文档的边界

- 官方文档与官方发布说明
- 内部仓库复原
- 大段 raw prompt 转录
- 无源码支撑的产品结论

## 需要保守书写的名称

下列名称即使出现在代码中，也保持源码字面和局部上下文范围：

- `Buddy`
- `KAIROS`
- `PROACTIVE`
- `voice`
- `TEAMMEM`
- `CHICAGO_MCP`
- `bridge`
- `remote isolation`

适合的写法包括：

- 代码里出现了相关名称或分支
- 当前镜像提供了局部线索
- 更强的产品化结论需要额外证据
- 公开 rollout 状态仍待独立确认

## 引用建议

引用这组文档时，建议同时保留这三条：

1. 这是非官方研究文档
2. 源码事实边界是公开镜像与本地 `_upstream` 镜像
3. feature gates 与隐藏分支属于代码路径线索，它们本身不足以说明公开能力

## 写作规则

- 重要结论尽量挂回源码路径
- `PROMPTS/` 解释装配机制，避免贴大段 raw prompt
- `FEATURE-FLAGS/` 记录代码中的 gate 与条件分支
- 证据较弱的地方优先缩小表述范围
