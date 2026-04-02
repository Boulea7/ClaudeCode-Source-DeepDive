[简体中文](./README.md) | [English](./README.en.md) | [繁體中文](./README.zh-TW.md) | [日本語](./README.ja.md)

# Claude Code Source Deep Dive

An unofficial research repository built around the public `Claude Code` source mirror.

The main question this repository answers is how the two entry paths branching from `main.tsx` converge into a shared `query/runtime` chain, and how tools, MCP, skills, plugins, permissions, memory, compaction, tasks, and prompts attach to that chain.

## What You Can Verify Here

- how the interactive path moves from `main.tsx` into `launchRepl()`, `REPL.tsx`, and then `query()`
- how the non-interactive / SDK path moves from `main.tsx` into `QueryEngine.ts` and then `query()`
- how `Tool.ts` and `tools.ts` define the tool contract, the built-in tool set, and the MCP-merged tool pool
- how `query.ts` handles tool execution, attachments, compaction, stop hooks, continuation rules, and between-turn refreshes
- which conclusions are already source-backed and which names or branches still need conservative wording

## Start Here

| Goal | Entry | What you get |
| --- | --- | --- |
| Build the big picture first | [ARCHITECTURE.en.md](./ARCHITECTURE.en.md) | the two entry paths, the shared runtime chain, and key entry files |
| Read by subsystem | [MODULES/README.en.md](./MODULES/README.en.md) | overview, simple guides, and deep dives for 8 modules |
| Focus on prompt assembly | [PROMPTS/README.en.md](./PROMPTS/README.en.md) | system prompt, agent prompt, and skill injection paths |
| Focus on gated branches | [FEATURE-FLAGS/README.en.md](./FEATURE-FLAGS/README.en.md) | compile-time gates, runtime gates, and conditional path clues |
| Scan the repo quickly | [SIMPLE/README.en.md](./SIMPLE/README.en.md) | a short route for first-time readers |
| Jump into source-heavy reading | [DEEP/README.en.md](./DEEP/README.en.md) | a longer route for source walkthroughs |

## Reading Paths

### Path A: Build the map first

1. [ARCHITECTURE.en.md](./ARCHITECTURE.en.md)
2. [MODULES/README.en.md](./MODULES/README.en.md)
3. any module `README.en.md`
4. any module `SIMPLE/README.en.md`
5. any module `DEEP/README.en.md`

### Path B: Follow the shared runtime chain

1. [ARCHITECTURE.en.md](./ARCHITECTURE.en.md)
2. [01-agent-loop-and-teams/README.en.md](./MODULES/01-agent-loop-and-teams/README.en.md)
3. [02-planning-compaction-and-assistant/README.en.md](./MODULES/02-planning-compaction-and-assistant/README.en.md)
4. [03-persistent-memory-system/README.en.md](./MODULES/03-persistent-memory-system/README.en.md)
5. [05-tools-mcp-skills-and-plugins/README.en.md](./MODULES/05-tools-mcp-skills-and-plugins/README.en.md)
6. [06-permissions-sandbox-and-trust/README.en.md](./MODULES/06-permissions-sandbox-and-trust/README.en.md)

### Path C: Start with prompts, gates, and remote-facing paths

1. [PROMPTS/README.en.md](./PROMPTS/README.en.md)
2. [FEATURE-FLAGS/README.en.md](./FEATURE-FLAGS/README.en.md)
3. [07-remote-session-bridge-and-sdk/README.en.md](./MODULES/07-remote-session-bridge-and-sdk/README.en.md)
4. [08-prompts-config-and-other-moats/README.en.md](./MODULES/08-prompts-config-and-other-moats/README.en.md)

## Key Docs And Folders

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

For a first pass, start with `README`, `ARCHITECTURE`, `MODULES`, `PROMPTS`, and `FEATURE-FLAGS`. `AI-AGENT/` is a structured companion layer for automation-oriented reading.

## Boundary Notes

- this is an unofficial research repository
- source-backed claims are bounded by `ChinaSiro/claude-code-sourcemap` and the local `_upstream/claude-code-sourcemap/` mirror
- `feature()`, GrowthBook, and env gates show conditional paths in code; they do not prove public rollout on their own
- names such as `Buddy`, `KAIROS`, `PROACTIVE`, `voice`, `bridge`, and `remote isolation` stay within source wording and surrounding context

See [DISCLAIMER.en.md](./DISCLAIMER.en.md) for the full boundary statement.

## Continue Reading

- [MODULES/README.en.md](./MODULES/README.en.md)
- [PROMPTS/README.en.md](./PROMPTS/README.en.md)
- [FEATURE-FLAGS/README.en.md](./FEATURE-FLAGS/README.en.md)
- [COMPARISONS/README.en.md](./COMPARISONS/README.en.md)
- [EXAMPLES/README.en.md](./EXAMPLES/README.en.md)
- [ASSETS/README.en.md](./ASSETS/README.en.md)
- [CONTRIBUTING.md](./CONTRIBUTING.md) / [CONTRIBUTING.en.md](./CONTRIBUTING.en.md)
- [SECURITY.md](./SECURITY.md) / [SECURITY.en.md](./SECURITY.en.md)
- [AI-AGENT](./AI-AGENT/): structured companion notes for automation-oriented reading
