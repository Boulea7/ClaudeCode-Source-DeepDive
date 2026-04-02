[简体中文](./README.md) | [English](./README.en.md) | [繁體中文](./README.zh-TW.md) | [日本語](./README.ja.md)

# Claude Code Source Deep Dive

一个围绕 `Claude Code` 公开镜像源码建立的非官方研究仓库。

这份仓库主要回答一类问题：`main.tsx` 分出的两个入口路径，怎样汇入共享的 `query/runtime` 主链，以及 tools、MCP、skills、plugins、permissions、memory、compact、tasks、prompts 等系统怎样挂到这条主链上。

## 你能在这里确认什么

- 交互式路径怎样从 `main.tsx` 进入 `launchRepl()`、`REPL.tsx`，再进入 `query()`
- 非交互 / SDK 路径怎样从 `main.tsx` 进入 `QueryEngine.ts`，再进入 `query()`
- `Tool.ts` 与 `tools.ts` 怎样定义工具协议、内建工具集合、MCP 合并后的工具池
- `query.ts` 怎样处理工具执行、attachments、compact、stop hooks、继续条件与跨回合刷新
- 哪些结论已经有源码支撑，哪些名称与分支仍需保守书写

## 从哪里开始读

| 目标 | 建议入口 | 你会得到什么 |
| --- | --- | --- |
| 先建立整体地图 | [ARCHITECTURE.md](./ARCHITECTURE.md) | 两个入口路径、共享主链、关键入口文件 |
| 按子系统阅读 | [MODULES/README.md](./MODULES/README.md) | 8 个模块的总览、简单版、深读版入口 |
| 只看 prompt 装配 | [PROMPTS/README.md](./PROMPTS/README.md) | system prompt、agent prompt、skill 注入路径 |
| 只看 gated 分支 | [FEATURE-FLAGS/README.md](./FEATURE-FLAGS/README.md) | 编译期 gate、运行时 gate、条件路径线索 |
| 快速浏览全仓 | [SIMPLE/README.md](./SIMPLE/README.md) | 面向第一次进入仓库的短路线 |
| 直接进入深读 | [DEEP/README.md](./DEEP/README.md) | 面向源码追读的长路线 |

## 推荐阅读路线

### 路线 A：先看整体图

1. [ARCHITECTURE.md](./ARCHITECTURE.md)
2. [MODULES/README.md](./MODULES/README.md)
3. 任意模块的 `README.md`
4. 任意模块的 `SIMPLE/README.md`
5. 任意模块的 `DEEP/README.md`

### 路线 B：先追共享主链

1. [ARCHITECTURE.md](./ARCHITECTURE.md)
2. [MODULES/01-agent-loop-and-teams](./MODULES/01-agent-loop-and-teams/)
3. [MODULES/02-planning-compaction-and-assistant](./MODULES/02-planning-compaction-and-assistant/)
4. [MODULES/03-persistent-memory-system](./MODULES/03-persistent-memory-system/)
5. [MODULES/05-tools-mcp-skills-and-plugins](./MODULES/05-tools-mcp-skills-and-plugins/)
6. [MODULES/06-permissions-sandbox-and-trust](./MODULES/06-permissions-sandbox-and-trust/)

### 路线 C：先看 prompts、gate 与远端路径

1. [PROMPTS/README.md](./PROMPTS/README.md)
2. [FEATURE-FLAGS/README.md](./FEATURE-FLAGS/README.md)
3. [MODULES/07-remote-session-bridge-and-sdk](./MODULES/07-remote-session-bridge-and-sdk/)
4. [MODULES/08-prompts-config-and-other-moats](./MODULES/08-prompts-config-and-other-moats/)

## 主要文档与目录

```text
.
├── README.md
├── README.en.md
├── README.zh-TW.md
├── README.ja.md
├── ARCHITECTURE.md
├── ARCHITECTURE.en.md
├── DISCLAIMER.md
├── DISCLAIMER.en.md
├── MODULES/
├── PROMPTS/
├── FEATURE-FLAGS/
├── SIMPLE/
├── DEEP/
├── COMPARISONS/
├── EXAMPLES/
├── ASSETS/
└── AI-AGENT/
```

首次阅读建议先看 `README`、`ARCHITECTURE`、`MODULES`、`PROMPTS`、`FEATURE-FLAGS`。`AI-AGENT/` 提供面向自动化阅读的结构化补充材料。

## 阅读边界

- 这是非官方研究仓库
- 源码事实边界是公开镜像 `ChinaSiro/claude-code-sourcemap` 与本地 `_upstream/claude-code-sourcemap/`
- `feature()`、GrowthBook、env gate 说明条件路径存在，它们本身不足以说明公开 rollout
- `Buddy`、`KAIROS`、`PROACTIVE`、`voice`、`bridge`、`remote isolation` 等名称保持源码字面和上下文范围

完整边界说明见 [DISCLAIMER.md](./DISCLAIMER.md)。

## 继续阅读

- [MODULES/README.md](./MODULES/README.md)
- [PROMPTS/README.md](./PROMPTS/README.md)
- [FEATURE-FLAGS/README.md](./FEATURE-FLAGS/README.md)
- [COMPARISONS/README.md](./COMPARISONS/README.md)
- [EXAMPLES/README.md](./EXAMPLES/README.md)
- [ASSETS/README.md](./ASSETS/README.md)
- [CONTRIBUTING.md](./CONTRIBUTING.md) / [CONTRIBUTING.en.md](./CONTRIBUTING.en.md)
- [SECURITY.md](./SECURITY.md) / [SECURITY.en.md](./SECURITY.en.md)
- [AI-AGENT](./AI-AGENT/)：面向自动化阅读的结构化补充材料
