# Runtime And Prompt Gates

## 这部分关注什么 gate

这一页只看：

- prompt 装配分支
- runtime 入口分支
- 交互层 / companion / voice 这类会直接影响模型可见能力或终端交互的 gate

如果你第一次读 feature gate，可以先把这页当成“主链上最常见的条件分支地图”。

## 关键文件

- `_upstream/claude-code-sourcemap/restored-src/src/main.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/screens/REPL.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/QueryEngine.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/query.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/constants/prompts.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/constants/systemPromptSections.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/systemPrompt.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/voice/voiceModeEnabled.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/hooks/useVoice.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/services/voiceStreamSTT.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/buddy/CompanionSprite.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/buddy/useBuddyNotification.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/buddy/prompt.ts`

## 代码里能确认的行为

### `CLAUDE_CODE_SIMPLE`

- `constants/prompts.ts` 会直接返回极简 prompt。
- `tools.ts` 会切到 simple mode tool 集合。
- 这说明 simple mode 同时改 prompt 和工具池，不只是 UI 瘦身。

### `COORDINATOR_MODE` + `CLAUDE_CODE_COORDINATOR_MODE`

- `utils/systemPrompt.ts` 会在特定条件下让 coordinator prompt 覆盖默认 prompt。
- `toolPool.ts` / `constants/tools.ts` 会切 coordinator mode 主线程工具集。
- `main.tsx` / `QueryEngine.ts` / `sessionRestore.ts` 还会在 headless、resume 和模式恢复路径里匹配 coordinator mode。
- 更稳妥的写法是：它同时作用于 prompt、context、tools、resume mode。
- 但这条 prompt 覆盖分支还要求当前没有 `mainThreadAgentDefinition`，所以不能把它写成“永远压过 main-thread agent”。

### `PROACTIVE` / `KAIROS` / `KAIROS_BRIEF` / `KAIROS_CHANNELS`

- `constants/prompts.ts` 在 proactive / KAIROS 激活时会走 autonomous prompt 路径，不再走标准 section registry。
- `utils/systemPrompt.ts` 会把 main-thread agent prompt 从“替换 default”改成“追加到 default 后面”。
- `main.tsx` 还会据此追加 proactive addendum、brief opt-in、assistant 相关状态。
- `cli/print.ts` 还能在 idle 时注入 `<tick>`，说明 `PROACTIVE` 不只是 prompt 分支。
- 这些名字在文档里更适合写成“源码里存在的运行时分支”，不是公开产品结论。

### `EXPERIMENTAL_SKILL_SEARCH`

- `constants/prompts.ts` 会在主线程 prompt 里加入 discover-skills 指导语。
- `query.ts` 会启动 skill discovery prefetch。
- 这说明它包含 prompt + query 两条分支。

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
- `/voice` 命令本身还会继续检查录音可用性、`voice_stream` 可用性、依赖和麦克风权限。
- 当前可见运行时里，`useVoice()` 的实际 caller 是 `useVoiceIntegration.tsx`，并且显式传入 `focusMode: false`。
- 当前检索范围里没有坐实 TTS / playback / output-side 主链，更适合写成“语音听写增强”。

### `tengu_cobalt_frost`

- `services/voiceStreamSTT.ts` 里有针对 Nova 3 的 gate 日志分支。
- 当前更准确的写法是：它会改写 `voice_stream` 的 query params，例如 `use_conversation_engine=true` 与 `stt_provider=deepgram-nova3`；这仍属于 STT 连接参数分支，不是 output-side 语音能力。

### `BUDDY`

- `buddy/CompanionSprite.tsx`、`useBuddyNotification.tsx`、`buddy/prompt.ts` 都直接受 `feature('BUDDY')` 控制。
- 当前能确认的是 companion sprite / notification / intro attachment 的 gated path。
- `REPL.tsx` 还会在 query 结束后调用 `fireCompanionObserver(...)`，把回调结果写进 `companionReaction`。
- `commands.ts` 里还能看到 `./commands/buddy/index.js` 的命令入口引用，但当前镜像未复核到对应实现文件。
- 但这轮没有在当前树里复核到 `fireCompanionObserver(...)` 的定义，也没有确认 `companionPetAt` 的写入点。
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

## 高风险误写点

- `KAIROS`
  - 当前源码能证明：会改写 prompt 路径，并和 brief / assistant 相关状态联动。
  - 当前不能证明：它在公开构建里对应一个稳定对外产品模式。
  - 推荐写法：`KAIROS` 是会改写 prompt / runtime 的 feature-gated 分支。
- `PROACTIVE`
  - 当前源码能证明：会让 main-thread agent prompt 从“替换 default”变成“追加到 default 后面”。
  - 当前不能证明：它已经固定等同于某个公开的 autonomous mode 档位。
  - 推荐写法：`PROACTIVE` 是 prompt / runtime 装配分支，不是发布公告。
- `Buddy`
  - 当前源码能证明：companion sprite、notification、intro attachment、reaction callback 路径存在。
  - 当前不能证明：observer 生成机制、pet 写入路径、正式产品命名与公开状态。
  - 推荐写法：`Buddy` 是 gated companion 前台表现层与 watcher 线索。
- `voice`
  - 当前源码能证明：开关、预检、本地录音、STT、输入框回填。
  - 当前不能证明：TTS、播放链、完整双向语音助手闭环。
  - 推荐写法：`voice` 当前更像 feature-gated 的语音听写增强链路。

## 推荐阅读顺序

1. `_upstream/claude-code-sourcemap/restored-src/src/constants/prompts.ts`
2. `_upstream/claude-code-sourcemap/restored-src/src/utils/systemPrompt.ts`
3. `_upstream/claude-code-sourcemap/restored-src/src/screens/REPL.tsx`
4. `_upstream/claude-code-sourcemap/restored-src/src/QueryEngine.ts`
5. `_upstream/claude-code-sourcemap/restored-src/src/query.ts`
6. `_upstream/claude-code-sourcemap/restored-src/src/voice/voiceModeEnabled.ts`
7. `_upstream/claude-code-sourcemap/restored-src/src/services/voiceStreamSTT.ts`
8. `_upstream/claude-code-sourcemap/restored-src/src/buddy/CompanionSprite.tsx`
