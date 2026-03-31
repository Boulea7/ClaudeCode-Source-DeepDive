Module 04 is best read as three separate code paths:

- `buddy/` is a companion subsystem, not a confirmed product-name layer.
- `vim/` is a real input-state machine with `types -> transitions -> motions -> operators/textObjects`.
- `voice/` confirms both gating and input/recording/STT integration points, but still should not be overstated as a fully confirmed end-to-end product stack.

Recommended order:
- `restored-src/src/buddy/companion.ts`
- `restored-src/src/buddy/CompanionSprite.tsx`
- `restored-src/src/buddy/prompt.ts`
- `restored-src/src/hooks/useVoiceIntegration.tsx`
- `restored-src/src/services/voiceStreamSTT.ts`
- `restored-src/src/hooks/useVimInput.ts`
- `restored-src/src/vim/types.ts`
- `restored-src/src/vim/transitions.ts`
- `restored-src/src/voice/voiceModeEnabled.ts`

Use this module when an agent needs:
- companion / watcher clues
- vim input behavior
- voice enablement conditions
- push-to-talk and transcript insertion surfaces
