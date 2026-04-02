[简体中文](./README.md) | [English](./README.en.md)

# 04 Buddy, Voice, Vim, And Terminal UI

This chapter explains how Claude Code’s terminal interaction layer reconnects companion surfaces, the voice input chain, and vim-style modal input back into the main interface.

In the public source mirror, this layer mainly lives in `screens/REPL.tsx`, `components/PromptInput/PromptInput.tsx`, `buddy/*`, `hooks/useVoiceIntegration.tsx`, `hooks/useVoice.ts`, `services/voice*.ts`, `hooks/useVimInput.ts`, `components/VimTextInput.tsx`, and `vim/*`. Those files are enough to show that the interaction layer is not only a shell. It is wired into input state, key handling, recording, STT, and companion UI.

## What You Should Understand After This Chapter

- what range `Buddy` should cover in the current source
- which input-side voice capabilities are supported, and which claims should stay out
- how vim-style modal input reconnects to `PromptInput`
- why `REPL.tsx` remains the interaction assembly point

## Key Files

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

## Where To Start

- quick guide: [SIMPLE/README.en.md](./SIMPLE/README.en.md)
- deep dive: [DEEP/README.en.md](./DEEP/README.en.md)
- short comparison: [comparison.en.md](./comparison.en.md)
