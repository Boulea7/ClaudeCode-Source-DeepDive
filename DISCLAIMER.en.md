[简体中文](./DISCLAIMER.md) | [English](./DISCLAIMER.en.md)

# Repository Disclaimer

## Repository Position

This document set is for reading the public source mirror, with focus on the runtime chain, module boundaries, tool systems, prompt assembly, and conditional paths.

Anthropic official structure, release timing, product naming, and internal repository content sit outside the factual scope of this document set.

## Boundary For Source Claims

All source-related conclusions in this repository come from these two places only:

- `https://github.com/ChinaSiro/claude-code-sourcemap`
- the local mirror: `_upstream/claude-code-sourcemap/`

When a claim cannot be checked against those two sources, this repository presents it as an inference, a clue, or an open question.

## What This Document Set Includes

- architecture overviews
- module-level source walkthroughs
- prompt assembly notes
- runtime notes for tools, MCP, skills, plugins, permissions, memory, compaction, tasks, and remote-related paths
- curated notes on feature gates and conditional branches

## Scope Boundary

- official documentation and official release notes
- reconstructed internal repositories
- large raw prompt dumps
- product conclusions without source support

## Names That Require Conservative Wording

Even when these names appear in source, they stay within source wording and local context:

- `Buddy`
- `KAIROS`
- `PROACTIVE`
- `voice`
- `TEAMMEM`
- `CHICAGO_MCP`
- `bridge`
- `remote isolation`

Safer phrasing includes:

- the code contains the name or branch
- the current mirror provides partial clues
- stronger product claims need more evidence
- public rollout status still needs separate confirmation

## Citation Guidance

If you quote this repository, keep these three points with it:

1. this is an unofficial research document set
2. source-backed claims are bounded by the public mirror and the local `_upstream` mirror
3. feature gates and hidden branches are code-path clues; they do not establish public capabilities on their own

## Writing Rules

- point important conclusions back to source paths when possible
- `PROMPTS/` explains assembly mechanisms and avoids large raw prompt dumps
- `FEATURE-FLAGS/` records code gates and conditional branches
- narrow the wording when evidence is incomplete
