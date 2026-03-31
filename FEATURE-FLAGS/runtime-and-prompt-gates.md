# Runtime And Prompt Gates

## 这部分关注什么 gate

这一页只看：

- prompt 装配分支
- runtime 入口分支
- 交互层 / companion / voice 这类会直接影响模型可见能力或终端交互的 gate

## 关键文件

- `restored-src/src/main.tsx`
- `restored-src/src/screens/REPL.tsx`
- `restored-src/src/QueryEngine.ts`
- `restored-src/src/query.ts`
- `restored-src/src/constants/prompts.ts`
- `restored-src/src/constants/systemPromptSections.ts`
- `restored-src/src/utils/systemPrompt.ts`
- `restored-src/src/voice/voiceModeEnabled.ts`
- `restored-src/src/services/voiceStreamSTT.ts`
- `restored-src/src/buddy/CompanionSprite.tsx`
- `restored-src/src/buddy/useBuddyNotification.tsx`
- `restored-src/src/buddy/prompt.ts`

## 代码里能确认的行为

### `CLAUDE_CODE_SIMPLE`

- `constants/prompts.ts` 会直接返回极简 prompt。
- `tools.ts` 会切到 simple mode tool 集合。
- 这说明 simple mode 同时改 prompt 和工具池，不只是 UI 瘦身。

### `COORDINATOR_MODE` + `CLAUDE_CODE_COORDINATOR_MODE`

- `utils/systemPrompt.ts` 会在特定条件下让 coordinator prompt 覆盖默认 prompt。
- `tools.ts` 会切 coordinator mode 工具集。
- `main.tsx` / `QueryEngine.ts` 还会在 resume 和 headless 路径里匹配 coordinator mode。
- 更稳妥的写法是：它同时作用于 prompt、context、tools。

### `PROACTIVE` / `KAIROS` / `KAIROS_BRIEF` / `KAIROS_CHANNELS`

- `constants/prompts.ts` 在 proactive / KAIROS 激活时会走 autonomous prompt 路径，不再走标准 section registry。
- `utils/systemPrompt.ts` 会把 main-thread agent prompt 从“替换 default”改成“追加到 default 后面”。
- `main.tsx` 还会据此追加 proactive addendum、brief opt-in、assistant 相关状态。
- 这些名字在文档里更适合写成“源码里存在的运行时分支”，不是公开产品结论。

### `EXPERIMENTAL_SKILL_SEARCH`

- `constants/prompts.ts` 会在主线程 prompt 里加入 discover-skills 指导语。
- `query.ts` 会启动 skill discovery prefetch。
- 这说明它不是单纯多一个工具名，而是 prompt + query 双分支。

### `SYSTEM_PROMPT_DYNAMIC_BOUNDARY`

- `constants/prompts.ts` 里它只在 `shouldUseGlobalCacheScope()` 为真时插入。
- 它是 cache boundary，不是永远存在的固定段落。

### `mcp_instructions` 与 delta 分支

- `mcp_instructions` 通过 `DANGEROUS_uncachedSystemPromptSection(...)` 注册。
- `isMcpInstructionsDeltaEnabled()` 为真时，这段说明会改走 attachment/delta 路径，而不是 inline section。
- 文档不能把 MCP instructions 写死成唯一的 prompt 内联段。

### `TOKEN_BUDGET`

- `constants/prompts.ts` 会注入 token budget 行为约束。
- `query.ts` 会在未达目标时继续追加 meta user message。
- 它是 prompt 约束 + runtime continuation 的组合。

### `CONTEXT_COLLAPSE` / `REACTIVE_COMPACT` / `HISTORY_SNIP` / `CACHED_MICROCOMPACT`

- `query.ts` 里这些 gate 直接影响 preflight：snip、microcompact、context collapse、auto compact 的触发条件。
- `REACTIVE_COMPACT` 还能抑制 proactive autocompact。
- 这些都属于 query-time context shaping，不是 prompt 静态能力。

### `VOICE_MODE` + `tengu_amber_quartz_disabled`

- `voice/voiceModeEnabled.ts` 把 voice 可见性拆成编译期开关和 GrowthBook kill switch。
- `hasVoiceAuth()` 还要求 Claude.ai OAuth。
- `isVoiceModeEnabled()` 最终是 auth + gate 的合成结果。

### `tengu_cobalt_frost`

- `services/voiceStreamSTT.ts` 里有针对 Nova 3 的 gate 日志分支。
- 当前可以写成 STT 连接参数和模型侧能力仍受运行时 gate 控制。

### `BUDDY`

- `buddy/CompanionSprite.tsx`、`useBuddyNotification.tsx`、`buddy/prompt.ts` 都直接受 `feature('BUDDY')` 控制。
- 当前能确认的是 companion sprite / notification / intro attachment 的 gated path。
- 不能把这组分支直接写成完整 companion 产品闭环。

## 不能确认的发布状态

- `KAIROS`、`PROACTIVE`、`COORDINATOR_MODE` 当前源码里确实有分支，但静态镜像不能证明它们在所有构建里都对外可用。
- `VOICE_MODE` 当前能确认 UI、预检、录音与 STT 接点，但不能仅凭这些文件推出完整语音产品范围。
- `BUDDY` 当前能确认 companion 子系统的前台表现层，但不能确认是否等于某个正式公开名称。

## 容易误写的点

- 不要把 `SYSTEM_PROMPT_DYNAMIC_BOUNDARY` 写成“每次都会注入”。
- 不要把 proactive / KAIROS 写成“就是 Claude Code 当前公开的 agent 模式”。
- 不要把 `VOICE_MODE` 写成“语音功能已经完整上线”。
- 不要把 `BUDDY` 写成“官方 companion 产品已经公开”。

## 推荐阅读顺序

1. `restored-src/src/constants/prompts.ts`
2. `restored-src/src/utils/systemPrompt.ts`
3. `restored-src/src/screens/REPL.tsx`
4. `restored-src/src/QueryEngine.ts`
5. `restored-src/src/query.ts`
6. `restored-src/src/voice/voiceModeEnabled.ts`
7. `restored-src/src/services/voiceStreamSTT.ts`
8. `restored-src/src/buddy/CompanionSprite.tsx`
