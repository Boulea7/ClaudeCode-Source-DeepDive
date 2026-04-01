[简体中文](./README.md) | [English](./README.en.md) | [繁體中文](./README.zh-TW.md) | [日本語](./README.ja.md)

# Claude Code Source Deep Dive

一个以源码拆解为核心的 `Claude Code` 非官方研究仓库。

这里的重点始终是三件事：

- 运行链如何接起来
- 模块之间如何分层
- 哪些结论已经有源码支撑，哪些地方仍需保守描述

## 你能在这里确认什么

- 交互式主线程怎样从 `main.tsx` 进入 `REPL.tsx`，再进入 `query.ts`
- `QueryEngine.ts` 在非交互 / SDK 路径中承担什么角色
- tools、MCP、skills、plugins、permissions、memory、compact、tasks 如何接到同一条运行链上
- prompt 装配、feature gate、remote / bridge 相关代码目前能确认到什么程度

## 这个仓库如何使用源码

- 代码事实只来自：
  - `https://github.com/ChinaSiro/claude-code-sourcemap`
  - 本地镜像：`_upstream/claude-code-sourcemap/`
- 本仓库中引用的源码路径，默认指向当前仓库里真实存在的：
  - `_upstream/claude-code-sourcemap/restored-src/src/...`

更完整的边界说明见 [DISCLAIMER.md](./DISCLAIMER.md)。

## 从哪里开始读

| 目标 | 建议入口 | 你会得到什么 |
| --- | --- | --- |
| 先建立整体地图 | [ARCHITECTURE.md](./ARCHITECTURE.md) | 主执行链、分层关系、关键入口文件 |
| 按模块系统阅读 | [MODULES/README.md](./MODULES/README.md) | 8 个模块的总览、简单版、深读版入口 |
| 只看 prompt 装配 | [PROMPTS/README.md](./PROMPTS/README.md) | system prompt、agent prompt、skill 注入路径 |
| 只看 gated 分支 | [FEATURE-FLAGS/README.md](./FEATURE-FLAGS/README.md) | 编译期 gate、运行时 gate、隐藏能力线索 |
| 快速浏览全仓 | [SIMPLE/README.md](./SIMPLE/README.md) | 面向第一次进入仓库的短路线 |
| 直接进入深读 | [DEEP/README.md](./DEEP/README.md) | 面向源码追读的长路线 |

## 推荐阅读路线

### 路线 A：先看整张图

1. [ARCHITECTURE.md](./ARCHITECTURE.md)
2. [MODULES/README.md](./MODULES/README.md)
3. 任意模块的 `SIMPLE/README.md`
4. 任意模块的 `DEEP/README.md`

### 路线 B：先看主运行链

1. [ARCHITECTURE.md](./ARCHITECTURE.md)
2. [MODULES/01-agent-loop-and-teams](./MODULES/01-agent-loop-and-teams/)
3. [MODULES/02-planning-compaction-and-assistant](./MODULES/02-planning-compaction-and-assistant/)
4. [MODULES/03-persistent-memory-system](./MODULES/03-persistent-memory-system/)
5. [MODULES/05-tools-mcp-skills-and-plugins](./MODULES/05-tools-mcp-skills-and-plugins/)
6. [MODULES/06-permissions-sandbox-and-trust](./MODULES/06-permissions-sandbox-and-trust/)

### 路线 C：先看 prompt、gate 与隐藏分支

1. [PROMPTS/README.md](./PROMPTS/README.md)
2. [FEATURE-FLAGS/README.md](./FEATURE-FLAGS/README.md)
3. [MODULES/08-prompts-config-and-other-moats](./MODULES/08-prompts-config-and-other-moats/)
4. [MODULES/07-remote-session-bridge-and-sdk](./MODULES/07-remote-session-bridge-and-sdk/)

## 仓库结构

```text
.
├── README.md
├── README.en.md
├── README.zh-TW.md
├── README.ja.md
├── DISCLAIMER.md
├── ARCHITECTURE.md
├── SIMPLE/
├── DEEP/
├── MODULES/
├── PROMPTS/
├── FEATURE-FLAGS/
├── COMPARISONS/
├── EXAMPLES/
└── ASSETS/
```

## 阅读时需要记住的边界

- 这是非官方研究仓库，不代表 Anthropic 官方结构、发布计划或产品口径
- `feature()`、GrowthBook、env gate 只能说明代码里存在条件分支，不能直接说明公开 rollout
- `Buddy`、`KAIROS`、`PROACTIVE`、`voice`、`bridge`、`remote isolation` 等名称只按源码证据保守书写
- `SYSTEM_PROMPT_DYNAMIC_BOUNDARY`、`mcp_instructions` 等 prompt 片段都要按条件路径理解，不能写成固定常驻段落

## 继续阅读

- [MODULES/README.md](./MODULES/README.md)
- [PROMPTS/README.md](./PROMPTS/README.md)
- [FEATURE-FLAGS/README.md](./FEATURE-FLAGS/README.md)
- [COMPARISONS/README.md](./COMPARISONS/README.md)
- [EXAMPLES/README.md](./EXAMPLES/README.md)

## 机器可读索引

如果你需要给其他 agent 喂结构化材料，可以再看：

- [AI-AGENT](./AI-AGENT/)
