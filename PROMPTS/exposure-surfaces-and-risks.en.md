[简体中文](./exposure-surfaces-and-risks.md) | [English](./exposure-surfaces-and-risks.en.md)

# Exposure Surfaces And Conservative Boundaries

This page explains the prompt-related areas that are easiest to overstate.

## What This Page Covers

- which areas can be explained at the mechanism level
- which areas are safer as source indexes only
- which names should remain gated-branch wording
- which attachments become model-visible context

## Mechanism-Level Surfaces

- `default prompt parts`
- `dynamic sections`
- `SYSTEM_PROMPT_DYNAMIC_BOUNDARY`
- interactive and non-interactive main-thread prompt paths
- ordinary and fork subagent prompt paths
- `skill_listing` and `command_permissions` attachments

## Index-Only Surfaces

- large raw system prompt dumps
- large raw agent prompt dumps
- large skill-body dumps
- internal helpers or rollout semantics that are not fully settled by the current mirror

## High-Risk Misstatements

- describing `SYSTEM_PROMPT_DYNAMIC_BOUNDARY` as always present
- describing `mcp_instructions` as one fixed inline section
- describing fork as fully identical to the parent thread
- turning `Buddy`, `KAIROS`, or `PROACTIVE` into fixed public modes

## Conservative Boundaries For This Section

- explain assembly mechanisms
- do not dump full raw prompts
- treat feature gates as code branches
- keep rollout wording conservative
