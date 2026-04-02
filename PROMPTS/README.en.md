[简体中文](./README.md) | [English](./README.en.md)

# PROMPTS

This document set tracks prompt assembly, prompt injection entry points, source anchors, and review boundaries in the current mirror.

## Reading Order

1. [system-prompt-assembly.en.md](./system-prompt-assembly.en.md)
2. [system-prompt-sections.en.md](./system-prompt-sections.en.md)
3. [agent-prompts.en.md](./agent-prompts.en.md)
4. [skills-and-command-injection.en.md](./skills-and-command-injection.en.md)
5. [exposure-surfaces-and-risks.en.md](./exposure-surfaces-and-risks.en.md)
6. [system-prompt-source-index.en.md](./system-prompt-source-index.en.md)

## Term Cards

- `gate`
  - A compile-time or runtime branch switch. Seeing a gate in source proves a branch exists. It does not prove rollout.
- `rollout`
  - The actual release state for a gated path in a build, account tier, subscription tier, or experiment cohort. Static source alone cannot prove rollout.
- `attachment-backed delta path`
  - A runtime path that sends changes through attachments instead of inlining them into the main system prompt sections. The directly confirmed example in this pass is `mcp_instructions_delta` in `attachments.ts`.
- `ordinary subagent`
  - A subagent path with an explicit `subagent_type`. It starts from the agent's own prompt source and then applies env/details enhancement.
- `fork subagent`
  - The implicit fork path triggered when `FORK_SUBAGENT` is enabled and `subagent_type` is omitted. It preferentially reuses the parent `renderedSystemPrompt` and message prefix.
- `dynamic boundary`
  - `SYSTEM_PROMPT_DYNAMIC_BOUNDARY`, the conditional marker that separates the cacheable static prefix from session-variant sections.

## Scope Boundary

- These pages explain assembly mechanics, injection paths, visibility surfaces, and conservative wording rules.
- They do not dump large raw system prompts or raw agent prompts.
- They do not convert feature gates into rollout claims.
- They keep fork, ordinary subagent, interactive main thread, and non-interactive main thread as separate paths.

## Main Source Spine Re-read In This Pass

- `_upstream/claude-code-sourcemap/restored-src/src/constants/prompts.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/constants/systemPromptSections.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/systemPrompt.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/queryContext.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/screens/REPL.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/QueryEngine.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/AgentTool.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/runAgent.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/forkSubagent.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/attachments.ts`
