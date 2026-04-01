[简体中文](./remote-bridge-and-session-gates.md) | [English](./remote-bridge-and-session-gates.en.md)

# Remote, Bridge, And Session Gates

This page collects the gates around remote sessions, bridge paths, CCR modes, and adjacent remote-agent behavior.

## What This Page Covers

- remote session client gates
- bridge / remote-control gates
- env-based, env-less, mirror, and adjacent remote backend gates

## Main Points

- `BRIDGE_MODE` is the compile-time bridge master switch
- `tengu_ccr_bridge` is an entitlement gate, not a blanket public capability
- `tengu_bridge_repl_v2` only switches REPL implementation paths
- env-based and env-less bridge paths stay distinct
- `connectRemoteControl()` still needs conservative wording

## Conservative Boundaries

- `/bridge` fields remain client-visible contract clues
- bridge wording should stay on the local outgoing bridge side
- transport variants should not become backend-architecture claims
