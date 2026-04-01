[简体中文](./system-prompt-sections.md) | [English](./system-prompt-sections.en.md)

# Dynamic Sections And Cache Boundaries

This page explains the section system itself: how dynamic prompt sections are registered, cached, invalidated, and recomputed.

## What This Page Explains

- how sections are registered
- what `cacheBreak` means
- how `resolveSystemPromptSections()` evaluates sections
- why `/clear` and `/compact` invalidate section state

## Main Points

- section entries are first-class registry objects
- uncached sections still write their latest value back to cache slots
- `mcp_instructions` is one of the clearest uncached sections in the standard registry path
- `SYSTEM_PROMPT_DYNAMIC_BOUNDARY` separates cacheable static content from runtime-sensitive content on qualifying paths

## Conservative Boundaries

- section registry is stable; section membership and content remain conditional
- `mcp_instructions` can move between inline sections and delta / attachment paths
- dynamic boundary wording should stay conditional
