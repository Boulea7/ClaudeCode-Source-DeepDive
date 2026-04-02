[简体中文](./system-prompt-assembly.md) | [English](./system-prompt-assembly.en.md)

# System Prompt Assembly

This page stays on system prompt assembly paths and dynamic rewrite points.

## Key Source Files

- `_upstream/claude-code-sourcemap/restored-src/src/constants/prompts.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/constants/systemPromptSections.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/systemPrompt.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/queryContext.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/screens/REPL.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/QueryEngine.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/attachments.ts`

## Confirmed From Source

- `prompts.ts:getSystemPrompt()` has three main paths:
  - the `CLAUDE_CODE_SIMPLE` minimal path
  - the standard path
  - the proactive path, gated by `PROACTIVE` or `KAIROS` plus an active proactive runtime
- The standard path returns a static prefix first and then appends registry-managed dynamic sections.
- The static prefix consistently includes intro, system, actions, tool-use guidance, tone/style, and output-efficiency guidance. `doing tasks` is inserted only when `outputStyleConfig === null` or `keepCodingInstructions === true`.
- `SYSTEM_PROMPT_DYNAMIC_BOUNDARY` is inserted only when `shouldUseGlobalCacheScope()` is true.
- `systemPromptSections.ts` defines two section types:
  - `systemPromptSection()`, which is cached
  - `DANGEROUS_uncachedSystemPromptSection()`, which can recompute per turn and may break cache stability
- `resolveSystemPromptSections()` reads from the section cache. The cache is cleared on `/clear` and `/compact` related reset paths.
- The standard dynamic section registry currently includes at least:
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
  - gated `numeric_length_anchors`
  - gated `token_budget`
  - gated `brief`
- `mcp_instructions` has two paths:
  - the inline section path
  - the attachment-backed delta path from `attachments.ts:getMcpInstructionsDeltaAttachment()`
- The interactive main thread in `REPL.tsx` uses `buildEffectiveSystemPrompt()`.
- The non-interactive main thread in `QueryEngine.ts` uses `fetchSystemPromptParts()` and `asSystemPrompt([...])`, so it does not directly call `buildEffectiveSystemPrompt()`.

## Not Confirmed From Source

- Which dynamic sections are enabled by default in a public build.
- The exact final section order and bytes in any live session.
- Rollout state for `PROACTIVE`, `KAIROS`, and `brief`.

## Review Checklist

- Keep `SYSTEM_PROMPT_DYNAMIC_BOUNDARY` conditional.
- Keep both the inline and attachment-backed delta paths for `mcp_instructions`.
- Keep interactive and non-interactive assembly paths separate.
- Avoid raw prompt dumps.
