[简体中文](./README.md) | [English](./README.en.md)

# Browse The Repository By Subsystem

This page splits the repository into 8 modules so you can start with a question, then follow the relevant source-backed paths.

## How To Use This Page

- pick a module by question first
- read the module `README.md` to set scope
- continue into `SIMPLE/README.md` or `DEEP/README.md` as needed
- when a topic crosses module boundaries, jump back to [ARCHITECTURE.en.md](../ARCHITECTURE.en.md) and compare against the shared runtime chain

## Suggested Reading Order

1. [01-agent-loop-and-teams](./01-agent-loop-and-teams/README.en.md)
2. [02-planning-compaction-and-assistant](./02-planning-compaction-and-assistant/README.en.md)
3. [03-persistent-memory-system](./03-persistent-memory-system/README.en.md)
4. [05-tools-mcp-skills-and-plugins](./05-tools-mcp-skills-and-plugins/README.en.md)
5. [06-permissions-sandbox-and-trust](./06-permissions-sandbox-and-trust/README.en.md)
6. [04-buddy-voice-vim-and-terminal-ui](./04-buddy-voice-vim-and-terminal-ui/README.en.md)
7. [07-remote-session-bridge-and-sdk](./07-remote-session-bridge-and-sdk/README.en.md)
8. [08-prompts-config-and-other-moats](./08-prompts-config-and-other-moats/README.en.md)

## Module Guide

| Module | Focus | Start here when you want to see |
| --- | --- | --- |
| [01-agent-loop-and-teams](./01-agent-loop-and-teams/README.en.md) | main loop, agents, teams, tasks | the entry into the execution chain |
| [02-planning-compaction-and-assistant](./02-planning-compaction-and-assistant/README.en.md) | plan mode, compaction, todos, assistant-related paths | how context is organized and reduced mid-run |
| [03-persistent-memory-system](./03-persistent-memory-system/README.en.md) | SessionMemory, team memory, memory extraction | how state persists across turns |
| [04-buddy-voice-vim-and-terminal-ui](./04-buddy-voice-vim-and-terminal-ui/README.en.md) | companion UI, voice, vim, terminal input | the REPL interaction and UX layer |
| [05-tools-mcp-skills-and-plugins](./05-tools-mcp-skills-and-plugins/README.en.md) | tools, MCP, skills, plugins | extension mechanisms and tool-pool assembly |
| [06-permissions-sandbox-and-trust](./06-permissions-sandbox-and-trust/README.en.md) | permissions, sandbox, approvals | execution boundaries and trust rules |
| [07-remote-session-bridge-and-sdk](./07-remote-session-bridge-and-sdk/README.en.md) | remote sessions, bridge, SDK | remote and non-interactive paths |
| [08-prompts-config-and-other-moats](./08-prompts-config-and-other-moats/README.en.md) | prompts, config, dynamic boundary | prompt assembly and conditional paths |

## How To Continue Inside Each Module

- `README.en.md`
  - start with module scope, key files, and entry relationships
- `SIMPLE/README.en.md`
  - build the mental model first
- `DEEP/README.en.md`
  - follow the source in more detail
- `comparison.en.md`
  - compare common summaries against the source-backed version

## Supplemental Material

- [../AI-AGENT](../AI-AGENT/) : structured companion notes for automation-oriented reading
