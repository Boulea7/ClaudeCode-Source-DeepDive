# Disclaimer

## 目的

本仓库只用于源码研究、架构拆解与开发者文档整理。

这里关注的是：

- `Claude Code` 的源码结构
- 运行时执行链
- prompt / tool / memory / permission / remote 等模块之间的关系

这里不做的事：

- 不发布完整还原源码
- 不把外部文章写成源码事实
- 不把 feature gate 名称写成公开产品公告

## 源码事实边界

本仓库中所有源码相关结论，只以以下两处为准：

- `https://github.com/ChinaSiro/claude-code-sourcemap`
- 本地镜像 `_upstream/claude-code-sourcemap/`

如果某个点在当前公开镜像里证据不足，文档只会写成：

- 有代码线索
- 当前镜像未完全坐实
- 不能过度下结论

## 与官方关系

本仓库是非官方研究仓库，与 Anthropic 无隶属关系，也不代表任何官方内部仓库结构、发布计划或产品口径。

## 文档内容边界

本仓库会整理：

- 架构总览
- 模块级源码走读
- prompt 装配机制
- feature flag / hidden branch 线索

本仓库不会整理：

- 大段 raw prompt
- 无源码支撑的竞品结论
- 把客户端兼容逻辑写成服务端事实

## 使用建议

如果你把这里的内容继续引用到别处，建议一并保留下面三条：

1. 这是非官方研究文档。
2. 源码结论以公开镜像为边界。
3. gated branch 不等于正式公开功能。
