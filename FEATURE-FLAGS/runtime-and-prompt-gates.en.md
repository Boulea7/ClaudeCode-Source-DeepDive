[简体中文](./runtime-and-prompt-gates.md) | [English](./runtime-and-prompt-gates.en.md)

# Runtime And Prompt Gates

This page tracks the gates that directly reshape prompt assembly, runtime entry paths, and user-facing interaction surfaces.

## Key Source Files

- `_upstream/claude-code-sourcemap/restored-src/src/main.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/screens/REPL.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/QueryEngine.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/query.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/constants/prompts.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/constants/systemPromptSections.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/systemPrompt.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/voice/voiceModeEnabled.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/services/voiceStreamSTT.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/buddy/CompanionSprite.tsx`

## Confirmed From Source

- `CLAUDE_CODE_SIMPLE` switches `getSystemPrompt()` into a minimal path.
- `SYSTEM_PROMPT_DYNAMIC_BOUNDARY` is inserted conditionally through `shouldUseGlobalCacheScope()`.
- `COORDINATOR_MODE` rewrites the main-thread priority branch in `buildEffectiveSystemPrompt()`.
- `PROACTIVE` and `KAIROS` reshape both the proactive `getSystemPrompt()` path and the way main-thread agent instructions are combined in `buildEffectiveSystemPrompt()`.
- In `query.ts`, `REACTIVE_COMPACT`, `CONTEXT_COLLAPSE`, `CACHED_MICROCOMPACT`, `TOKEN_BUDGET`, `HISTORY_SNIP`, and `BG_SESSIONS` continue to reshape query-time context handling.
- `VOICE_MODE` is safest to describe as a voice-input or dictation-enhancement path. This pass did not confirm a full two-way voice assistant.
- `tengu_cobalt_frost` is currently confirmed only as a `voice_stream` query-parameter branch.
- `BUDDY` is currently confirmed only across companion sprite, notification, intro attachment, and reaction-style front-end paths.

## Not Confirmed From Source

- Public rollout for `KAIROS`, `PROACTIVE`, or `COORDINATOR_MODE`.
- The full product scope behind `VOICE_MODE`.
- Whether `Buddy` equals an already public product name.

## Review Checklist

- Keep `SYSTEM_PROMPT_DYNAMIC_BOUNDARY` conditional.
- Do not expand `VOICE_MODE` into TTS or a full voice assistant.
- Do not expand `Buddy` into a publicly settled companion product.
- Keep prompt-path gates separate from rollout claims.
