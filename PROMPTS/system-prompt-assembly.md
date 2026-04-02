[简体中文](./system-prompt-assembly.md) | [English](./system-prompt-assembly.en.md)

# System Prompt Assembly

这一页只讲 system prompt 的装配路径与动态改写点。

## 关键源码文件

- `_upstream/claude-code-sourcemap/restored-src/src/constants/prompts.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/constants/systemPromptSections.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/systemPrompt.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/queryContext.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/screens/REPL.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/QueryEngine.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/attachments.ts`

## 当前源码能确认的机制

- `prompts.ts:getSystemPrompt()` 有三条主路径：
  - `CLAUDE_CODE_SIMPLE` 的极简路径
  - standard path
  - proactive path。条件是 `PROACTIVE` 或 `KAIROS` 分支存在，且 proactive runtime 处于活动状态
- standard path 先返回静态前缀，再按 section registry 追加动态段落。
- 静态前缀稳定包含 intro、system、actions、tool use、tone/style、output efficiency；`doing tasks` 只在 `outputStyleConfig === null` 或 `keepCodingInstructions === true` 时插入。
- `SYSTEM_PROMPT_DYNAMIC_BOUNDARY` 只会在 `shouldUseGlobalCacheScope()` 为真时插入。
- `systemPromptSections.ts` 定义了两类 section：
  - `systemPromptSection()`。结果会缓存
  - `DANGEROUS_uncachedSystemPromptSection()`。结果允许逐轮重算并可能打破缓存
- `resolveSystemPromptSections()` 会读取 section cache。缓存结果在 `/clear` 与 `/compact` 相关清理路径后重置。
- 当前标准动态 sections 至少包括：
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
- `mcp_instructions` 有两条路径：
  - inline section path
  - `attachments.ts:getMcpInstructionsDeltaAttachment()` 提供的 attachment-backed delta path
- interactive main thread 在 `REPL.tsx` 里使用 `buildEffectiveSystemPrompt()`。
- non-interactive main thread 在 `QueryEngine.ts` 里用 `fetchSystemPromptParts()` 与 `asSystemPrompt([...])` 自己拼装，不直接调用 `buildEffectiveSystemPrompt()`。

## 当前源码不能确认的内容

- 哪些 dynamic sections 在某个公开构建里默认打开。
- 某次真实会话里所有 section 的最终字节顺序和具体文本。
- `PROACTIVE`、`KAIROS`、`brief` 等路径的 rollout 状态。

## 复核清单

- `SYSTEM_PROMPT_DYNAMIC_BOUNDARY` 是否仍写成条件插入。
- `mcp_instructions` 是否同时保留 inline 与 delta attachment 两条路径。
- interactive 与 non-interactive 装配链是否被分开。
- 文档里是否避免了 raw prompt 转储。
