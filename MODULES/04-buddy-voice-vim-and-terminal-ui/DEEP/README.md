# 深度拆解：Buddy, Voice, Vim, And Terminal UI

这一章最重要的做法是：**只写源码里能确认的部分，少猜产品包装名。**

## 可以确认的部分

### 1. `buddy/` 是真实目录

可直接看到：

- `restored-src/src/buddy/CompanionSprite.tsx`
- `restored-src/src/buddy/companion.ts`
- `restored-src/src/buddy/prompt.ts`
- `restored-src/src/buddy/useBuddyNotification.tsx`

这至少说明：

- companion / sprite / notification 是被单独实现的
- 这不是外部文档里的幻想名词

### 2. `voice/` 和 `vim/` 都是独立模块

可直接看到：

- `restored-src/src/voice/voiceModeEnabled.ts`
- `restored-src/src/vim/motions.ts`
- `restored-src/src/vim/operators.ts`
- `restored-src/src/vim/textObjects.ts`
- `restored-src/src/vim/transitions.ts`

这说明：

- vim mode 不是一个简单布尔开关
- 它内部至少有 motion、operator、text object、transition 这类对象

### 3. UI 和 agent 协作相连

`buddy/useBuddyNotification.tsx`、`tools/AgentTool/UI.tsx` 这些文件说明：  
Claude Code 的 UI 并不只是单人输入输出窗口，它会直接展示 agent 相关状态。

## 建议阅读顺序

1. `restored-src/src/buddy/CompanionSprite.tsx`
2. `restored-src/src/buddy/useBuddyNotification.tsx`
3. `restored-src/src/vim/types.ts`
4. `restored-src/src/vim/transitions.ts`
5. `restored-src/src/tools/AgentTool/UI.tsx`

## 谨慎点

本仓库会写：

- `buddy/` 是真实源码目录
- 它和 companion / notification / prompt 有关

本仓库不会轻易写：

- `Buddy` 在产品层面就一定等于某个公开命名功能

因为这个判断在当前公开镜像里还不够稳。

