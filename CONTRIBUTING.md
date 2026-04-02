[简体中文](./CONTRIBUTING.md) | [English](./CONTRIBUTING.en.md)

# 贡献说明

感谢你愿意改进这个仓库。

这是一份以源码拆解为核心的研究型文档仓库。贡献时最重要的目标有两个：

- 保持源码事实准确
- 保持人类文档清楚、克制、可复核

## 贡献前先确认

- 源码相关结论只来自以下两处：
  - `https://github.com/ChinaSiro/claude-code-sourcemap`
  - 本地镜像：`_upstream/claude-code-sourcemap/`
- 下结论前请重新读源码，不要沿用旧文档里的未经复核判断
- 证据不足时请缩小表述范围，不要把代码线索写成产品事实

## 文档写作规则

- 中文优先保持友好、克制、清楚，少用黑话
- 英文镜像应自然、准确，不要写成机器翻译腔
- 人类文档保持中英文双版本同步
- `PROMPTS/` 解释装配机制，不贴大段 raw prompt
- `Buddy`、`KAIROS`、`voice`、`bridge`、`remote isolation` 等名称要保守书写
- `feature()`、GrowthBook、env gate 只能说明条件路径存在，不能直接说明公开 rollout
- 避免使用“不……而是……”“不……只……”这类转折句式，优先改成直接陈述句

## 目录范围

- 欢迎改动：
  - 根级人类文档
  - `MODULES/`
  - `PROMPTS/`
  - `FEATURE-FLAGS/`
  - `COMPARISONS/`
  - `SIMPLE/`
  - `DEEP/`
  - `EXAMPLES/`
  - `ASSETS/`
- 默认不要改动：
  - `AI-AGENT/`
- 不要提交：
  - `TASK_GOAL.md`
  - `agents.md`
  - `_upstream/`

## 提交前检查

- 确认导航链接与中英文镜像同步
- 确认源码路径仍指向 `_upstream/claude-code-sourcemap/restored-src/src/...`
- 运行 `git diff --check`
- 如果改的是纯文档，可以不跑测试，但请在交付说明里明确写：
  - `本轮没有跑测试，原因是文档改写`

## Pull Request 建议

- 标题尽量直接说明改动范围
- 描述里建议写清：
  - 改了哪些页面
  - 是否涉及源码结论收紧
  - 是否补了英文镜像或导航
  - 做了哪些最小校验
