[简体中文](./skills-and-command-injection.md) | [English](./skills-and-command-injection.en.md)

# Skills And Command Injection

这一页记录 skill 从目录与命令注册表进入模型可见上下文的链路。

## 关键源码文件

- `_upstream/claude-code-sourcemap/restored-src/src/skills/loadSkillsDir.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/commands.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/SkillTool/SkillTool.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/processUserInput/processSlashCommand.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/attachments.ts`

## 当前源码能确认的机制

- `loadSkillsDir.ts` 里 `parseSkillFrontmatterFields()` 负责解析 skill frontmatter。
- `loadSkillsDir.ts` 里 `createSkillCommand()` 把 skill 变成统一的 `Command` 结构。
- `loadSkillsDir.ts` 同时维护 `conditionalSkills` 与 `dynamicSkills`。
- `discoverSkillDirsForPaths()` 与 `activateConditionalSkillsForPaths()` 会按路径把技能加入动态集合。
- `commands.ts:getSkillToolCommands()` 给 SkillTool prompt listing 提供集合。过滤条件包括：
  - `type === 'prompt'`
  - `!disableModelInvocation`
  - `source !== 'builtin'`
  - skills/bundled/legacy commands 直接保留
  - plugin 命令需要显式描述信息
- `commands.ts:getMcpSkillCommands()` 单独从 `AppState.mcp.commands` 里取出 `loadedFrom === 'mcp'` 的 prompt skills。
- `commands.ts:getSlashCommandToolSkills()` 维护另一组技能索引集合。它和 `getSkillToolCommands()` 不是同一个结果集。
- `SkillTool.ts:getAllCommands()` 会把本地命令集合与 MCP skills 合并。它明确排除 plain MCP prompts，只保留 `loadedFrom === 'mcp'` 的 prompt skills。
- `SkillTool.ts:validateInput()` 会校验 skill 是否存在、是否为 prompt command、是否被 `disableModelInvocation` 禁止。
- `SkillTool.ts` 在 `command.context === 'fork'` 时会走 forked skill 执行链；其他 prompt skills 走 `processPromptSlashCommand()`。
- `processPromptSlashCommand()` 会生成：
  - loading metadata message
  - 展开的 skill 正文 message
  - 从 skill 内容里继续解析出来的 attachment messages
  - `command_permissions` attachment
- `attachments.ts:getSkillListingAttachments()` 会把本地 skills 与 MCP skills 合并，并以 `skill_listing` attachment 发送增量可见面。

## 当前源码不能确认的内容

- 任意一次真实会话里所有 skills 的完整最终 listing。
- remote skill search 在所有构建里的 rollout 状态。
- 某个 plugin marketplace 规则在公开构建里的统一策略。

## 复核清单

- 是否把执行集合、listing 集合、skills 索引集合混成一个集合。
- 是否把 SkillTool 写成 discovery 源。
- 是否漏掉 `command_permissions` attachment。
- 是否漏掉 `skill_listing` 对本地 skills 与 MCP skills 的合并路径。
