[简体中文](./exposure-surfaces-and-risks.md) | [English](./exposure-surfaces-and-risks.en.md)

# Exposure Surfaces And Risks

这一页定义 PROMPTS 文档里允许写到什么程度。

## 关键源码文件

- `_upstream/claude-code-sourcemap/restored-src/src/constants/prompts.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/queryContext.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/processUserInput/processSlashCommand.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/AgentTool.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/forkSubagent.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/attachments.ts`

## 当前源码能确认的可见面

- `getSystemPrompt()` 返回的 system prompt 片段数组。
- `buildEffectiveSystemPrompt()` 与 `QueryEngine.ts` 组装出的主线程 system prompt。
- `processPromptSlashCommand()` 展开的 skill 正文、loading metadata、attachment messages 和 `command_permissions` attachment。
- `attachments.ts` 生成并注入的 attachment message。当前本轮直接复核到的类型包括：
  - `mcp_instructions_delta`
  - `skill_listing`
  - `command_permissions`
  - `task_status`
- fork child 的消息前缀。它来自 `buildForkedMessages()` 生成的 assistant message 与占位 `tool_result`。

## 当前源码能确认的高风险误写点

- `SYSTEM_PROMPT_DYNAMIC_BOUNDARY` 是条件插入，不是每轮恒定存在的段落。
- `mcp_instructions` 既有 inline section path，也有 attachment-backed delta path。
- ordinary subagent 与 fork subagent 的 prompt 来源不同。
- `createAttachmentMessage()` 会把 attachment 变成实际消息对象。文档可以解释 attachment 类型和注入入口。
- `command_permissions` 属于 skill 执行后的附加权限说明，入口在 `processPromptSlashCommand()`。

## 当前源码不能确认的内容

- 任意一次真实会话里的完整 raw prompt。
- `Buddy`、`KAIROS`、`PROACTIVE` 等名字对应的公开产品命名和 rollout。
- 任何服务端侧策略、实验分桶和 entitlement 规则。

## 复核清单

- 是否把 attachment 说成了 system prompt section。
- 是否把 gated branch 说成了 rollout 事实。
- 是否把 fork path 写成和父线程绝对一致。
- 是否转储了大段 raw prompt 或完整 skill body。
