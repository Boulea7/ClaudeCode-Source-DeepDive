# 深度拆解：Permissions, Sandbox, And Trust

这一章最重要的结论是：**Claude Code 的信任模型是多层的。**

## 可以直接从源码看到的几层

### 1. 规则层

`restored-src/src/utils/permissions/` 很丰富，关键文件包括：

- `permissions.ts`
- `permissionSetup.ts`
- `permissionsLoader.ts`
- `PermissionMode.ts`
- `permissionRuleParser.ts`
- `filesystem.ts`
- `pathValidation.ts`
- `yoloClassifier.ts`

这说明权限系统不是只有一个 if 判断，而是一个成体系的规则层。

### 2. UI 层

`components/permissions/` 目录非常大，说明审批不是一个统一弹窗，而是按工具类型做了专门界面。

例如：

- `PermissionRequest.tsx`
- `PermissionPrompt.tsx`
- `BashPermissionRequest/`
- `FileEditPermissionRequest/`
- `EnterPlanModePermissionRequest/`
- `SandboxPermissionRequest.tsx`

### 3. MCP 审批层

`services/mcpServerApproval.tsx` 很值得单独看。它说明项目级 `.mcp.json` server 不是自动放进运行时，而是有专门审批流程。

## 建议阅读顺序

1. `restored-src/src/utils/permissions/permissions.ts`
2. `restored-src/src/utils/permissions/permissionSetup.ts`
3. `restored-src/src/components/permissions/PermissionRequest.tsx`
4. `restored-src/src/components/permissions/BashPermissionRequest/`
5. `restored-src/src/services/mcpServerApproval.tsx`

## 这一章最值得记住的一句话

Claude Code 的安全边界不是一个单点提示，而是规则、审批和运行时限制一起工作。

