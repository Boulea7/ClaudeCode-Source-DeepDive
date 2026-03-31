# 深度拆解：Planning, Compaction, And Assistant

这一章最重要的结论是：**Claude Code 把 planning 做成了运行时对象，而不是临时对话文本。**

## 关键证据

### 1. `EnterPlanModeTool` 和 `ExitPlanModeTool`

从目录结构就能看出，进入和退出 `Plan Mode` 是独立工具，而不是散落在 UI 里的开关。

重点文件：

- `tools/EnterPlanModeTool/EnterPlanModeTool.ts`
- `tools/ExitPlanModeTool/ExitPlanModeV2Tool.ts`

### 2. `utils/plans.ts`

这部分说明计划文件本身是持久工件：

- 每个 session 会生成 slug
- 计划文件可恢复
- 计划不是只存在于消息历史里

### 3. `compact.ts`

`services/compact/compact.ts` 很关键，因为它告诉我们：

- 上下文压缩不是“清空重来”
- 计划引用会被保留
- skill 和 mode 的上下文也会被重新挂回去

### 4. `QueryEngine.ts`

`assistant/` 目录本身并不大，但 `QueryEngine.ts` 很大。说明真正的运行时主体更靠近 query loop，而不是某个单独的 assistant 目录。

## 建议阅读顺序

1. `restored-src/src/tools/EnterPlanModeTool/EnterPlanModeTool.ts`
2. `restored-src/src/commands/plan/plan.tsx`
3. `restored-src/src/utils/plans.ts`
4. `restored-src/src/services/compact/compact.ts`
5. `restored-src/src/QueryEngine.ts`

## 关于 `KAIROS`

源码里能看到 `KAIROS` 作为 feature flag 的痕迹。  
但当前公开镜像不足以把它写成一个完整、清晰可见的独立子系统。

所以这类说法在本仓库里应当标记为：**有代码线索，但不能过度下结论。**

