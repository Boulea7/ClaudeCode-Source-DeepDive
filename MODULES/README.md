[简体中文](./README.md) | [English](./README.en.md)

# 按子系统浏览仓库

这一页把全仓拆成 8 个模块，方便按问题进入，再回到源码路径继续追读。

## 这页怎么用

- 先按问题选一个模块
- 先看模块 `README.md` 建立范围感
- 再按需要进入 `SIMPLE/README.md` 或 `DEEP/README.md`
- 需要跨模块时，回到 [ARCHITECTURE.md](../ARCHITECTURE.md) 对照共享主链

## 建议阅读顺序

1. [01-agent-loop-and-teams](./01-agent-loop-and-teams/)
2. [02-planning-compaction-and-assistant](./02-planning-compaction-and-assistant/)
3. [03-persistent-memory-system](./03-persistent-memory-system/)
4. [05-tools-mcp-skills-and-plugins](./05-tools-mcp-skills-and-plugins/)
5. [06-permissions-sandbox-and-trust](./06-permissions-sandbox-and-trust/)
6. [04-buddy-voice-vim-and-terminal-ui](./04-buddy-voice-vim-and-terminal-ui/)
7. [07-remote-session-bridge-and-sdk](./07-remote-session-bridge-and-sdk/)
8. [08-prompts-config-and-other-moats](./08-prompts-config-and-other-moats/)

## 模块导航

| 模块 | 重点 | 什么时候先看 |
| --- | --- | --- |
| [01-agent-loop-and-teams](./01-agent-loop-and-teams/) | 主循环、agent、team、tasks | 想先追执行链入口 |
| [02-planning-compaction-and-assistant](./02-planning-compaction-and-assistant/) | plan mode、compact、todo、assistant 相关路径 | 想看中途怎样整理与压缩上下文 |
| [03-persistent-memory-system](./03-persistent-memory-system/) | SessionMemory、team memory、memory 提取 | 想看状态怎样跨回合保留 |
| [04-buddy-voice-vim-and-terminal-ui](./04-buddy-voice-vim-and-terminal-ui/) | companion UI、voice、vim、终端输入 | 想看 REPL 交互层与体验层 |
| [05-tools-mcp-skills-and-plugins](./05-tools-mcp-skills-and-plugins/) | tools、MCP、skills、plugins | 想看扩展机制与工具池装配 |
| [06-permissions-sandbox-and-trust](./06-permissions-sandbox-and-trust/) | permissions、sandbox、approval | 想看执行边界与信任模型 |
| [07-remote-session-bridge-and-sdk](./07-remote-session-bridge-and-sdk/) | remote session、bridge、SDK | 想看远端与非交互路径 |
| [08-prompts-config-and-other-moats](./08-prompts-config-and-other-moats/) | prompts、config、dynamic boundary | 想看系统提示词与条件路径 |

## 每个模块里怎么继续读

- `README.md`
  - 先看模块范围、关键文件、入口关系
- `SIMPLE/README.md`
  - 先建立心智模型
- `DEEP/README.md`
  - 再顺着源码追细节
- `comparison.md`
  - 最后对照常见说法与源码差异

## 补充材料

- [../AI-AGENT](../AI-AGENT/)：面向自动化阅读的结构化补充材料
