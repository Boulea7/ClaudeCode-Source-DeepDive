[简体中文](./README.md) | [English](./README.en.md)

# 04 Buddy, Voice, Vim, And Terminal UI

本章说明 Claude Code 的终端交互层如何把 companion surface、voice 输入链和 vim 模态输入接回主界面。

公开镜像里，这一层主要落在 `screens/REPL.tsx`、`components/PromptInput/PromptInput.tsx`、`buddy/*`、`hooks/useVoiceIntegration.tsx`、`hooks/useVoice.ts`、`services/voice*.ts`、`hooks/useVimInput.ts`、`components/VimTextInput.tsx` 与 `vim/*`。这些文件足以确认交互层不是单纯外壳。它已经接进输入状态、键位、录音、STT 和 companion UI。

## 读完这一章，你会更清楚什么

- `Buddy` 在当前源码里更适合写成什么范围
- voice 能确认到哪些输入侧能力，哪些能力不能外推
- vim 模态输入是如何接回 PromptInput 的
- `REPL.tsx` 为什么仍然是交互层总装配点

## 关键文件

- `_upstream/claude-code-sourcemap/restored-src/src/screens/REPL.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/components/PromptInput/PromptInput.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/buddy/companion.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/buddy/CompanionSprite.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/hooks/useVoiceIntegration.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/hooks/useVoiceEnabled.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/hooks/useVoice.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/voice/voiceModeEnabled.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/services/voice.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/services/voiceStreamSTT.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/hooks/useVimInput.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/components/VimTextInput.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/vim/`

## 从哪里开始读

- 快速版：[SIMPLE/README.md](./SIMPLE/README.md)
- 深度版：[DEEP/README.md](./DEEP/README.md)
- 轻量比较：[comparison.md](./comparison.md)
