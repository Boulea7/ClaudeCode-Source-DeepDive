Module 08 explains prompt assembly as runtime structure.

Focus on:
- `constants/prompts.ts` as the default section factory
- `constants/systemPromptSections.ts` as the cache / uncached section layer
- `utils/systemPrompt.ts` as the final precedence combiner
- `main.tsx`, `QueryEngine.ts`, and `runAgent.ts` as the places where those prompts are actually consumed

Key distinctions to preserve:
- interactive main thread vs non-interactive main thread
- normal subagent vs fork subagent
- default prompt generation vs effective prompt assembly
