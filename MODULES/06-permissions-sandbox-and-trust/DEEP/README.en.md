[简体中文](./README.md) | [English](./README.en.md)

# Deep Dive: Permissions, Sandbox, And Trust

This chapter explains how Claude Code turns tool approval into a layered trust model.

## What This Chapter Covers

- permission context setup
- rule and path decisions
- ask-flow orchestration
- approval UI dispatch

## Key Source Files

- `_upstream/claude-code-sourcemap/restored-src/src/utils/permissions/`
- `_upstream/claude-code-sourcemap/restored-src/src/hooks/useCanUseTool.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/hooks/toolPermission/handlers/interactiveHandler.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/components/permissions/`

## Main Points

- `permissionSetup.ts` prepares the permission context and mode state.
- `permissions.ts` produces structured decisions rather than a single boolean.
- `useCanUseTool` and `interactiveHandler` orchestrate ask flows.
- `PermissionRequest.tsx` dispatches already-computed requests to specific UI components.
- sandbox approval, tool approval, and project-level MCP server approval are related but separate chains.

## Conservative Boundaries

- classifier behavior should keep its feature/build conditions
- `PermissionRequest.tsx` should stay described as a dispatch surface, not the core decision engine
- MCP server approval should stay separate from ordinary per-tool approval

## Read Next

- [README.en.md](../README.en.md)
- [comparison.en.md](../comparison.en.md)
