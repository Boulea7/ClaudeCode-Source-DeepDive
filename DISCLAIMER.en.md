[简体中文](./DISCLAIMER.md) | [English](./DISCLAIMER.en.md)

# Disclaimer

## Repository Position

This is an unofficial, developer-facing research document set.

It records reading notes derived from the public source mirror, with the goal of making the runtime chain, module boundaries, and implementation details easier to verify.

## Boundary For Code Claims

All source-backed claims in this repository come only from:

- `https://github.com/ChinaSiro/claude-code-sourcemap`
- the local mirror: `_upstream/claude-code-sourcemap/`

If a statement cannot be checked against those two sources, this repository does not present it as a code fact.

## What This Repository Includes

- architecture overviews
- module-level source walkthroughs
- prompt assembly notes
- runtime notes for tools, MCP, skills, plugins, permissions, memory, compaction, tasks, and remote behavior
- curated notes on feature gates and hidden capability clues

## What This Repository Does Not Include

- official documentation
- official release notes
- a reconstructed internal repository
- large raw prompt dumps
- product conclusions without source support

## Names That Must Stay Conservative

Even when the names appear in source, they should stay source-bound and conservative:

- `Buddy`
- `KAIROS`
- `PROACTIVE`
- `voice`
- `TEAMMEM`
- `CHICAGO_MCP`
- `bridge`
- `remote isolation`

Preferred wording includes:

- code clues exist
- the current mirror does not fully settle this
- stronger conclusions would go too far
- public rollout status cannot be confirmed

## Relationship To Official Sources

This repository has no formal relationship with Anthropic and does not represent official internal structure, product naming, or release timing.

Its analysis reflects reading notes from the public mirror only.

## Citation Guidance

If you quote this repository, keep these three points:

1. this is an unofficial research document set
2. code facts are bounded by the public mirror and the local `_upstream` mirror
3. feature gates and hidden branches do not equal publicly released capabilities

## Writing Rules

- important claims should point back to source paths when possible
- `PROMPTS/` explains assembly mechanisms and does not dump large raw prompts
- `FEATURE-FLAGS/` records code gates and branches, not rollout announcements
- uncertain points should be written narrowly
