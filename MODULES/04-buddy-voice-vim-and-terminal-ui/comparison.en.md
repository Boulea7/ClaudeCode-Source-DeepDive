[简体中文](./comparison.md) | [English](./comparison.en.md)

# Short Comparison

Many AI coding tools focus on the editor surface.

Claude Code is more explicit at this layer:

- the terminal has a companion surface
- voice is already wired into an input-side recording and STT chain
- vim-style modal input has its own state machine and execution layer
- those interaction capabilities are all routed back through `REPL.tsx` and `PromptInput.tsx`
