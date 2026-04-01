[简体中文](./system-prompt-assembly.md) | [English](./system-prompt-assembly.en.md)

# Main-Thread Prompt Assembly

This page explains how Claude Code assembles the system prompt across the main-thread paths and agent variants.

## What This Page Explains

- how `getSystemPrompt()` produces default prompt parts
- how the interactive main thread assembles the effective prompt
- how the non-interactive path differs
- how ordinary subagents and fork subagents diverge

## Key Source Files

- `_upstream/claude-code-sourcemap/restored-src/src/constants/prompts.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/constants/systemPromptSections.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/systemPrompt.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/queryContext.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/screens/REPL.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/QueryEngine.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/runAgent.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/forkSubagent.ts`

## Main Points

- `getSystemPrompt()` returns prompt parts, not one final string.
- `SYSTEM_PROMPT_DYNAMIC_BOUNDARY` is inserted only on qualifying paths.
- the interactive main thread uses `buildEffectiveSystemPrompt()` in `REPL.tsx`
- the non-interactive path assembles `custom/default + memoryMechanics? + append` in `QueryEngine.ts`
- ordinary subagents use their own prompt origin
- fork subagents preferentially reuse the parent’s rendered prompt and prefix

## Conservative Boundaries

- `dynamic boundary` must stay conditional in wording
- proactive / KAIROS / coordinator branches remain feature-gated paths, not rollout claims
- fork reuse should not be described as byte-for-byte guaranteed identity
