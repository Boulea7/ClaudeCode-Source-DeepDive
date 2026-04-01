[简体中文](./README.md) | [English](./README.en.md)

# FEATURE-FLAGS

This section collects the gates and hidden branches that can change runtime behavior in the source.

## What This Section Covers

- compile-time gates such as `feature()`
- runtime gates from GrowthBook and env switches
- conditional branches across prompts, memory, agents, remote, bridge, voice, and companion surfaces

## Suggested Reading Order

1. [runtime-and-prompt-gates.en.md](./runtime-and-prompt-gates.en.md)
2. [agent-memory-compact-gates.en.md](./agent-memory-compact-gates.en.md)
3. [remote-bridge-and-session-gates.en.md](./remote-bridge-and-session-gates.en.md)

## Boundary Notes

- a gate in code does not prove public rollout
- a name in code does not prove a public product name
- compile-time gates and runtime gates should stay separate
- names such as `Buddy`, `KAIROS`, `PROACTIVE`, `voice`, `bridge`, and `remote isolation` must remain conservative
