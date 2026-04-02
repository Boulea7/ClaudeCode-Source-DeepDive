[简体中文](./ARCHITECTURE.md) | [English](./ARCHITECTURE.en.md)

# Claude Code Architecture Overview

This page gives a source-backed map before you dive into module details.

The current public mirror shows two main entry paths branching from `main.tsx`, and both converge into a shared `query/runtime` chain.

## Two Entry Paths, One Shared Runtime Chain

- interactive main thread:
  - `main.tsx -> launchRepl() -> REPL.tsx -> query()`
- non-interactive / SDK path:
  - `main.tsx -> QueryEngine.ts -> query()`

The shared runtime surface across those paths includes:

- the tool pool
- prompt assembly and context loading
- permissions and approvals
- memory and compaction
- tasks and agent runtime
- MCP, skills, and plugins
- attachments, stop hooks, and continuation rules

## Key Entry Files

The source paths you can open directly in this repository live under:

- `_upstream/claude-code-sourcemap/restored-src/src/main.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/screens/REPL.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/QueryEngine.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/query.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/Tool.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools.ts`

## One Diagram For The Whole Flow

```mermaid
flowchart LR
    A[main.tsx] --> B{entry path}
    B --> C[launchRepl()]
    B --> D[QueryEngine.ts]
    C --> E[REPL.tsx]
    E --> G[query()]
    D --> G
    G --> H[tool execution and attachments]
    G --> I[memory and compaction]
    G --> J[permissions and approvals]
    G --> K[tasks and agent runtime]
    E --> L[prompt assembly and interactive context]
    D --> M[prompt assembly and transcript state]
    E --> N[tool pool and MCP merge]
```

## What Each Layer Handles

### Startup And Wiring

`main.tsx` handles CLI startup, config and model preparation, permission context, MCP-related initialization, and bundled plugin / skill registration. Interactive sessions then enter `launchRepl()`. Headless and SDK flows take the `QueryEngine.ts` wrapper path.

### Interactive Orchestration Layer

`REPL.tsx` is the core orchestration layer for the interactive path. In source, it reads fresh tools and MCP clients from current store state, assembles the effective system prompt, and directly drives the shared query loop with `for await ... of query(...)`. Describing it as a viewer alone would miss a key source-backed role.

### Non-Interactive / SDK Wrapper

`QueryEngine.ts` is also a wrapper around `query(...)`. It manages message state, prompt parts, transcript handling, and structured IO concerns, then enters the same shared query loop with `querySource: 'sdk'`.

### Shared Query Loop

`query.ts` is the shared turn execution core. It owns loop state, handles tool execution, attachment injection, compaction, stop hooks, continuation rules, and between-turn refreshes of tools and context.

### Tool Contract And Tool Pool

`Tool.ts` defines the shared tool contract and `ToolUseContext`. `tools.ts` assembles the concrete tool pool: `getTools()` handles built-in tools plus filtering rules, while `assembleToolPool()` combines built-in tools and MCP tools into the runtime pool.

## Boundary Notes For This Page

- `REPL.tsx` and `QueryEngine.ts` both enter the same `query()` core, but they serve different entry responsibilities
- `ToolUseContext` carries runtime state and some REPL-only UI fields, so docs should keep UI-only state separate from API / transcript state
- the tool pool changes with deny rules, agent restrictions, feature gates, runtime state, and MCP connection state
- prompt fragments such as `SYSTEM_PROMPT_DYNAMIC_BOUNDARY` and `mcp_instructions` should be described as conditional path elements
- names such as `Buddy`, `KAIROS`, `voice`, `bridge`, and remote-related labels should stay within source wording and local context

## Where To Go Next

- for module-by-module reading:
  - [MODULES/README.en.md](./MODULES/README.en.md)
- for prompt assembly details:
  - [PROMPTS/README.en.md](./PROMPTS/README.en.md)
- for gate-focused reading:
  - [FEATURE-FLAGS/README.en.md](./FEATURE-FLAGS/README.en.md)
