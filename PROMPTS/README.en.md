[简体中文](./README.md) | [English](./README.en.md)

# PROMPTS

This set of documents explains Claude Code’s prompt assembly and injection paths.

It focuses on four question groups:

- where the default prompt parts come from
- how interactive and non-interactive main-thread paths assemble the system prompt
- how ordinary subagents and fork subagents differ in prompt origin
- how skills, attachments, and gates shape model-visible context

## Suggested Reading Order

1. [system-prompt-assembly.en.md](./system-prompt-assembly.en.md)
2. [agent-prompts.en.md](./agent-prompts.en.md)
3. [system-prompt-sections.en.md](./system-prompt-sections.en.md)
4. [skills-and-command-injection.en.md](./skills-and-command-injection.en.md)
5. [system-prompt-source-index.en.md](./system-prompt-source-index.en.md)
6. [exposure-surfaces-and-risks.en.md](./exposure-surfaces-and-risks.en.md)

## Term Notes

- `default prompt parts`
  - the prompt fragments returned by `getSystemPrompt()`
- `interactive main thread`
  - `main.tsx -> REPL.tsx -> query.ts`
- `non-interactive main thread`
  - `main.tsx -> QueryEngine.ts -> query.ts`
- `ordinary subagent`
  - uses the agent’s own prompt origin
- `fork subagent`
  - preferentially reuses the parent’s rendered prompt and message prefix
- `dynamic boundary`
  - the conditional `SYSTEM_PROMPT_DYNAMIC_BOUNDARY`

## What This Section Does Not Do

- it does not dump large raw prompts
- it does not turn feature-gated paths into rollout claims
- it does not present prompt assembly as one fixed universal pipeline
