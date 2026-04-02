[简体中文](./README.md) | [English](./README.en.md)

# Deep Dive: Permissions, Sandbox, And Trust

This chapter explains how Claude Code turns tool approval into a layered trust model.

## What This Chapter Covers

- permission context setup
- rule and path decisions
- ask-flow orchestration
- approval UI dispatch

## Key Source Files

- `_upstream/claude-code-sourcemap/restored-src/src/utils/permissions/permissionSetup.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/permissions/permissions.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/permissions/permissionRuleParser.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/permissions/filesystem.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/permissions/pathValidation.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/permissions/yoloClassifier.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/permissions/bashClassifier.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/hooks/useCanUseTool.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/hooks/toolPermission/handlers/interactiveHandler.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/components/permissions/PermissionRequest.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/components/permissions/`

## Execution Flow

### 1. `permissionSetup.ts` prepares the permission context

The current mirror supports a clear separation between setup and final decision.

`permissionSetup.ts` reads permission-related settings, folds rule sources into `ToolPermissionContext`, and carries mode-related state such as auto mode and plan mode transitions into later checks.

That is why it should stay described as a preparation layer. It is not the final allow / deny / ask engine on its own.

### 2. `permissions.ts` produces structured decisions

`permissions.ts` turns the current context and rule set into concrete results.

The result is more informative than a single boolean. The file supports rule matching across built-in tools and MCP-style names, and the decision reason can carry categories such as:

- `rule`
- `mode`
- `hook`
- `classifier`
- `sandboxOverride`
- `workingDir`

That is the key source-backed reason this system feels like a trust runtime rather than a thin safety check.

### 3. Ask-flow orchestration is a separate layer

Once the system reaches an `ask` outcome, the flow moves through `useCanUseTool.tsx` and the interactive handler chain.

This layer decides how the question is routed through:

- ordinary interactive approval
- coordinator or worker-specific paths
- hook and classifier-related branches
- remote or bridged approval handling where applicable

That means “the system decided to ask” and “the system knows how to ask” are two different responsibilities.

### 4. `PermissionRequest.tsx` is a dispatch surface

One boundary needs to stay explicit: `PermissionRequest.tsx` does not calculate the allow / ask / deny result.

Its role is to take an already computed request and dispatch it to a more specific UI component. The broader chain is:

1. setup and decision code prepares a structured result
2. `useCanUseTool` and `interactiveHandler` orchestrate ask-flow handling
3. `REPL.tsx` renders the permission request queue
4. `PermissionRequest.tsx` dispatches to tool-specific UI

That is why it should stay described as a dispatch and rendering surface, not as the core decision engine.

### 5. Approval UI is specialized, not one generic popup

The current mirror shows multiple specialized approval components for different request types, including Bash, file edit/write, entering or exiting plan mode, sandboxing, and other tool-specific flows.

This matters because the UI layer already encodes that not all requests should look or behave the same way. It is not a single generic yes/no dialog.

One extra boundary also matters here: `ExitPlanModePermissionRequest` is heavier than a pure presentational component because it participates in state-reset and resume-related branching. That is still a UI-layer special case, not proof that all permission UI is business logic.

## Why This Layer Matters

Claude Code does not treat trust as an afterthought. The current mirror shows a chain that can:

- merge rule sources
- switch modes
- run classifier-backed safety checks
- route ask flows through orchestration code
- render different approval UIs for different request classes
- keep sandboxing and MCP server approval adjacent but separate

That combination is why the permission system reads more like a runtime subsystem than a single modal.

## Conservative Boundaries

- keep classifier behavior tied to its feature and build conditions
- keep `PermissionRequest.tsx` described as a dispatch surface, not as the core decision engine
- keep MCP server approval separate from ordinary per-tool approval
- keep sandbox approval separate from the broader rule parser and mode state machinery

## Read Next

- [README.en.md](../README.en.md)
- [comparison.en.md](../comparison.en.md)
