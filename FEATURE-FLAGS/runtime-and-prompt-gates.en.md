[简体中文](./runtime-and-prompt-gates.md) | [English](./runtime-and-prompt-gates.en.md)

# Runtime And Prompt Gates

This page collects gates that directly affect prompt assembly, runtime entry paths, and major interaction surfaces.

## What This Page Covers

- prompt-path branches
- runtime entry branches
- interaction-facing gates for companion and voice surfaces

## Main Points

- `CLAUDE_CODE_SIMPLE` changes both prompt shape and tool-pool shape
- `COORDINATOR_MODE` changes prompt, tools, and resume behavior under specific conditions
- `PROACTIVE` and `KAIROS` change both prompt paths and runtime behavior
- `SYSTEM_PROMPT_DYNAMIC_BOUNDARY` remains conditional
- `VOICE_MODE` currently supports a conservative “voice dictation enhancement” description
- `BUDDY` currently supports a conservative companion-surface description

## Conservative Boundaries

- prompt-path gates do not prove public rollout
- `voice` should not expand into TTS or a full two-way assistant
- `Buddy` should not expand into a settled public product name
