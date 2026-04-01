[简体中文](./skills-and-command-injection.md) | [English](./skills-and-command-injection.en.md)

# How Skills Reach Commands And Context

This page explains how a `SKILL.md` file becomes a `Command`, then becomes model-visible context or executable skill behavior.

## What This Page Explains

- how skill files are parsed into `Command(type: 'prompt')`
- how listing and execution sets differ
- what `SkillTool` actually does
- when dynamic and conditional skills appear

## Main Points

- `loadSkillsDir.ts` produces commands; it does not execute them
- `commands.ts` exposes several different views: execution, listing, index, and MCP skill subsets
- `SkillTool` executes commands from the broader execution set
- `processPromptSlashCommand()` injects the resulting content back into the conversation
- `skill_listing` and `command_permissions` attachments are separate model-visible surfaces

## Conservative Boundaries

- `SkillTool` should stay described as an execution shell
- `getSkillToolCommands()` should stay narrower than the full execution set
- MCP skill discovery details should stay cautious unless the missing source pieces are re-read directly
