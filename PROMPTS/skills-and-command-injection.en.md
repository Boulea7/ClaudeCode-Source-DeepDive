[简体中文](./skills-and-command-injection.md) | [English](./skills-and-command-injection.en.md)

# Skills And Command Injection

This page tracks how skills move from directories and registries into model-visible context.

## Key Source Files

- `_upstream/claude-code-sourcemap/restored-src/src/skills/loadSkillsDir.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/commands.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/SkillTool/SkillTool.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/processUserInput/processSlashCommand.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/attachments.ts`

## Confirmed From Source

- `loadSkillsDir.ts:parseSkillFrontmatterFields()` parses skill frontmatter.
- `loadSkillsDir.ts:createSkillCommand()` turns a skill into the shared `Command` shape.
- `loadSkillsDir.ts` maintains both `conditionalSkills` and `dynamicSkills`.
- `discoverSkillDirsForPaths()` and `activateConditionalSkillsForPaths()` move skills into the dynamic set based on path activity.
- `commands.ts:getSkillToolCommands()` builds the SkillTool prompt listing set. It filters for:
  - `type === 'prompt'`
  - `!disableModelInvocation`
  - `source !== 'builtin'`
  - direct inclusion for skills, bundled skills, and legacy commands
  - explicit description requirements for plugin commands
- `commands.ts:getMcpSkillCommands()` separately extracts prompt-type MCP skills from `AppState.mcp.commands`.
- `commands.ts:getSlashCommandToolSkills()` is a different skills index and should not be flattened into the SkillTool listing set.
- `SkillTool.ts:getAllCommands()` merges local commands with MCP skills and explicitly excludes plain MCP prompts.
- `SkillTool.ts:validateInput()` verifies that the requested skill exists, is prompt-based, and is not blocked by `disableModelInvocation`.
- `SkillTool.ts` routes `command.context === 'fork'` into the forked-skill path. Other prompt skills go through `processPromptSlashCommand()`.
- `processPromptSlashCommand()` produces:
  - a loading metadata message
  - the expanded skill body message
  - attachment messages parsed from the expanded skill content
  - a `command_permissions` attachment
- `attachments.ts:getSkillListingAttachments()` merges local skills with MCP skills and sends them through `skill_listing` attachments.

## Not Confirmed From Source

- The complete final skill listing for any specific live session.
- Rollout state for remote skill search across all builds.
- A single public policy for every plugin marketplace path.

## Review Checklist

- Do not collapse the execution set, the SkillTool listing set, and the skills index into one set.
- Do not describe SkillTool as the discovery source.
- Do not omit the `command_permissions` attachment.
- Do not omit the merged local-skill plus MCP-skill path behind `skill_listing`.
