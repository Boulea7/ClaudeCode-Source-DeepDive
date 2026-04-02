[简体中文](./system-prompt-sections.md) | [English](./system-prompt-sections.en.md)

# System Prompt Sections

This page explains the section registry. It does not restate raw section bodies.

## Key Source Files

- `_upstream/claude-code-sourcemap/restored-src/src/constants/systemPromptSections.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/constants/prompts.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/sessionRestore.ts`

## Confirmed From Source

- `systemPromptSection(name, compute)` creates a cached section.
- `DANGEROUS_uncachedSystemPromptSection(name, compute, reason)` creates a per-turn recomputed section.
- `resolveSystemPromptSections()`:
  - returns cached values on cache hit
  - runs `compute()` on cache miss
  - stores the result back into the cache
- `clearSystemPromptSections()` clears the section cache and resets beta-header latches.
- Source comments explicitly tie section-cache reset to `/clear` and `/compact` flows.
- `prompts.ts` currently registers these main section names:
  - `session_guidance`
  - `memory`
  - `ant_model_override`
  - `env_info_simple`
  - `language`
  - `output_style`
  - `mcp_instructions`
  - `scratchpad`
  - `frc`
  - `summarize_tool_results`
  - `numeric_length_anchors`
  - `token_budget`
  - `brief`
- `mcp_instructions` is explicitly registered as `DANGEROUS_uncachedSystemPromptSection()`.

## Not Confirmed From Source

- Default-on status for any section in a public build.
- The final runtime body of any section.

## Review Checklist

- Do not describe the section cache as permanent.
- Do not omit `/clear` and `/compact` reset semantics.
- Do not downgrade `mcp_instructions` into an ordinary cached section.
