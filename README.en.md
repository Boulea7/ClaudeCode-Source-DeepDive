[简体中文](./README.md) | [English](./README.en.md) | [繁體中文](./README.zh-TW.md) | [日本語](./README.ja.md)

# Claude Code Source Deep Dive

An unofficial research repository focused on reading `Claude Code` through source-backed architecture notes.

This repository keeps the emphasis on three things:

- how the runtime chain is connected
- how major subsystems are split
- which statements are already grounded in source and which still require conservative wording

## What You Can Verify Here

- how the interactive main thread moves from `main.tsx` into `REPL.tsx`, then into `query.ts`
- what role `QueryEngine.ts` plays on non-interactive / SDK paths
- how tools, MCP, skills, plugins, permissions, memory, compaction, and tasks connect to the same runtime
- how far the current source supports prompt assembly, feature gates, and remote / bridge behavior

## How This Repository Uses Source

- Code claims come only from:
  - `https://github.com/ChinaSiro/claude-code-sourcemap`
  - the local mirror: `_upstream/claude-code-sourcemap/`
- Source paths in this repository point to the real local mirror path:
  - `_upstream/claude-code-sourcemap/restored-src/src/...`

See [DISCLAIMER.en.md](./DISCLAIMER.en.md) for the full boundary statement.

## Start Here

| Goal | Entry | What you get |
| --- | --- | --- |
| Build the big picture first | [ARCHITECTURE.en.md](./ARCHITECTURE.en.md) | the main execution chain, major layers, and key entry files |
| Read by subsystem | [MODULES/README.en.md](./MODULES/README.en.md) | overview, simple guides, and deep dives for 8 modules |
| Focus on prompt assembly | [PROMPTS/README.en.md](./PROMPTS/README.en.md) | system prompt, agent prompt, and skill injection paths |
| Focus on gated branches | [FEATURE-FLAGS/README.en.md](./FEATURE-FLAGS/README.en.md) | compile-time gates, runtime gates, and hidden capability clues |
| Scan the repo quickly | [SIMPLE/README.en.md](./SIMPLE/README.en.md) | a short route for first-time readers |
| Jump into source-heavy reading | [DEEP/README.en.md](./DEEP/README.en.md) | a longer route for source walkthroughs |

## Reading Paths

### Path A: Build the map first

1. [ARCHITECTURE.en.md](./ARCHITECTURE.en.md)
2. [MODULES/README.en.md](./MODULES/README.en.md)
3. any module `SIMPLE/README.en.md`
4. any module `DEEP/README.en.md`

### Path B: Follow the runtime chain

1. [ARCHITECTURE.en.md](./ARCHITECTURE.en.md)
2. [MODULES/01-agent-loop-and-teams](./MODULES/01-agent-loop-and-teams/)
3. [MODULES/02-planning-compaction-and-assistant](./MODULES/02-planning-compaction-and-assistant/)
4. [MODULES/03-persistent-memory-system](./MODULES/03-persistent-memory-system/)
5. [MODULES/05-tools-mcp-skills-and-plugins](./MODULES/05-tools-mcp-skills-and-plugins/)
6. [MODULES/06-permissions-sandbox-and-trust](./MODULES/06-permissions-sandbox-and-trust/)

### Path C: Focus on prompts, gates, and hidden branches

1. [PROMPTS/README.en.md](./PROMPTS/README.en.md)
2. [FEATURE-FLAGS/README.en.md](./FEATURE-FLAGS/README.en.md)
3. [MODULES/08-prompts-config-and-other-moats](./MODULES/08-prompts-config-and-other-moats/)
4. [MODULES/07-remote-session-bridge-and-sdk](./MODULES/07-remote-session-bridge-and-sdk/)

## Repo Map

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

## Boundary Notes

- This is an unofficial research repository. It does not represent Anthropic’s official structure, rollout plans, or product wording.
- `feature()`, GrowthBook, and env gates only show conditional code paths. They do not prove public rollout.
- Names such as `Buddy`, `KAIROS`, `PROACTIVE`, `voice`, `bridge`, and `remote isolation` stay source-bound and conservative.
- Prompt fragments such as `SYSTEM_PROMPT_DYNAMIC_BOUNDARY` and `mcp_instructions` must be described as conditional path elements, not fixed always-on sections.

## Continue Reading

- [MODULES/README.en.md](./MODULES/README.en.md)
- [PROMPTS/README.en.md](./PROMPTS/README.en.md)
- [FEATURE-FLAGS/README.en.md](./FEATURE-FLAGS/README.en.md)
- [COMPARISONS/README.en.md](./COMPARISONS/README.en.md)
- [EXAMPLES/README.en.md](./EXAMPLES/README.en.md)

## Machine-Readable Index

If you want structured material for other agents, see:

- [AI-AGENT](./AI-AGENT/)
