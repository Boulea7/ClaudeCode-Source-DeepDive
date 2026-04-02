[简体中文](./exposure-surfaces-and-risks.md) | [English](./exposure-surfaces-and-risks.en.md)

# Exposure Surfaces And Risks

This page defines how far the PROMPTS docs should go.

## Key Source Files

- `_upstream/claude-code-sourcemap/restored-src/src/constants/prompts.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/queryContext.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/processUserInput/processSlashCommand.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/AgentTool.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/forkSubagent.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/attachments.ts`

## Confirmed Exposure Surfaces

- The system prompt arrays returned by `getSystemPrompt()`.
- The assembled main-thread system prompt produced by `buildEffectiveSystemPrompt()` and `QueryEngine.ts`.
- Skill expansion from `processPromptSlashCommand()`, including the expanded text, loading metadata, attachment messages, and the `command_permissions` attachment.
- Attachment messages produced by `attachments.ts`. This pass directly re-checked:
  - `mcp_instructions_delta`
  - `skill_listing`
  - `command_permissions`
  - `task_status`
- Fork-child message prefixes produced by `buildForkedMessages()`, including the assistant message clone and placeholder `tool_result` blocks.

## Confirmed High-Risk Overstatements

- `SYSTEM_PROMPT_DYNAMIC_BOUNDARY` is conditional, not a guaranteed section on every turn.
- `mcp_instructions` has both an inline-section path and an attachment-backed delta path.
- Ordinary subagents and fork subagents do not share the same prompt origin.
- `createAttachmentMessage()` turns attachments into actual message objects, so attachment types and injection paths are valid mechanism-level documentation.
- `command_permissions` is attached after skill expansion through `processPromptSlashCommand()`.

## Not Confirmed From Source

- The full raw prompt for any real runtime turn.
- Public product names or rollout state for labels such as `Buddy`, `KAIROS`, and `PROACTIVE`.
- Server-side policy, experiment allocation, or entitlement rules.

## Review Checklist

- Do not describe attachments as system prompt sections.
- Do not describe gated branches as rollout facts.
- Do not describe fork paths as byte-for-byte identity with the parent.
- Do not paste large raw prompts or complete skill bodies.
