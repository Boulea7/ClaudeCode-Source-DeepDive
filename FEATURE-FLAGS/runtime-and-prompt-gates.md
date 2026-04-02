[简体中文](./runtime-and-prompt-gates.md) | [English](./runtime-and-prompt-gates.en.md)

# Runtime And Prompt Gates

这一页记录直接改写 prompt 装配、运行入口和前台交互面的 gate。

## 关键源码文件

- `_upstream/claude-code-sourcemap/restored-src/src/main.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/screens/REPL.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/QueryEngine.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/query.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/constants/prompts.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/constants/systemPromptSections.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/systemPrompt.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/voice/voiceModeEnabled.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/services/voiceStreamSTT.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/buddy/CompanionSprite.tsx`

## 当前源码能确认的行为

- `CLAUDE_CODE_SIMPLE` 会把 `getSystemPrompt()` 切到极简路径。
- `SYSTEM_PROMPT_DYNAMIC_BOUNDARY` 按 `shouldUseGlobalCacheScope()` 条件插入。
- `COORDINATOR_MODE` 会改写 `buildEffectiveSystemPrompt()` 的主线程优先级分支。
- `PROACTIVE` 与 `KAIROS` 会改写 `getSystemPrompt()` 的 proactive path，也会改写 `buildEffectiveSystemPrompt()` 中 main-thread agent prompt 的拼接方式。
- `query.ts` 里 `REACTIVE_COMPACT`、`CONTEXT_COLLAPSE`、`CACHED_MICROCOMPACT`、`TOKEN_BUDGET`、`HISTORY_SNIP`、`BG_SESSIONS` 都会继续改写 query-time context shaping。
- `VOICE_MODE` 当前更稳妥的表述是语音输入或听写增强链路。当前本轮没有把它扩展成完整双向语音助手。
- `tengu_cobalt_frost` 当前只坐实到 `voice_stream` query params 分支。
- `BUDDY` 当前只坐实到 companion sprite、notification、intro attachment、reaction callback 这类前台路径。

## 当前源码不能确认的内容

- `KAIROS`、`PROACTIVE`、`COORDINATOR_MODE` 的公开 rollout。
- `VOICE_MODE` 的完整产品范围。
- `Buddy` 是否等于某个已经公开发布的正式产品名。

## 复核清单

- `SYSTEM_PROMPT_DYNAMIC_BOUNDARY` 保持条件插入表述。
- `VOICE_MODE` 不扩写成 TTS 或完整语音助手。
- `Buddy` 不扩写成已经公开的完整 companion 产品。
- prompt path gate 和 rollout 结论继续分开。
