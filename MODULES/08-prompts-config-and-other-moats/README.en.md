[简体中文](./README.md) | [English](./README.en.md)

# 08 Prompts, Config, And Runtime Glue

This chapter collects prompt assembly, config impact, and several important mechanisms that are easier to explain together.

## What You Should Understand After This Chapter

- how the system prompt is assembled
- how config influences runtime behavior
- why `dynamic boundary` must stay conditional
- which startup decisions continue to shape later turns

## Key Files

- `_upstream/claude-code-sourcemap/restored-src/src/constants/prompts.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/constants/systemPromptSections.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/systemPrompt.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/queryContext.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/screens/REPL.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/QueryEngine.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/main.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/bootstrap/`

## Where To Start

- quick guide: [SIMPLE/README.en.md](./SIMPLE/README.en.md)
- deep dive: [DEEP/README.en.md](./DEEP/README.en.md)
- short comparison: [comparison.en.md](./comparison.en.md)
