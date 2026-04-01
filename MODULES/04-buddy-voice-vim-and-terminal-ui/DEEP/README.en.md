[简体中文](./README.md) | [English](./README.en.md)

# Deep Dive: Buddy, Voice, Vim, And Terminal UI

This chapter focuses on what the current source lets us say about terminal interaction surfaces.

## What This Chapter Covers

- companion-facing UI surfaces
- the voice input chain as far as the source settles it
- the layered vim-style modal input implementation

## Key Source Files

- `_upstream/claude-code-sourcemap/restored-src/src/buddy/`
- `_upstream/claude-code-sourcemap/restored-src/src/voice/voiceModeEnabled.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/services/voice.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/services/voiceStreamSTT.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/vim/`
- `_upstream/claude-code-sourcemap/restored-src/src/components/PromptInput/PromptInput.tsx`

## Main Points

- `Buddy` is best described as a companion / watcher surface clue backed by gated UI code.
- the current source settles a voice dictation-enhancement chain: gate checks, preflight, local recording, STT, and input reinsertion.
- the vim implementation is a layered modal input engine, not a claim of full Vim parity.

## Conservative Boundaries

- do not expand `Buddy` into a settled public product name
- do not expand voice coverage into TTS, playback, or a full two-way voice assistant
- keep `/buddy` command behavior and reaction generation narrower unless those files are re-read directly

## Read Next

- [README.en.md](../README.en.md)
- [comparison.en.md](../comparison.en.md)
