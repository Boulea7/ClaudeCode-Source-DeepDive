# FEATURE-FLAGS

这一组文档只做一件事：

**把源码里被 gate、被隐藏、未必正式发布的能力单独摘出来。**

这里不做的事：

- 不把 gate 名字直接写成产品公告
- 不把客户端分支写成服务端事实
- 不把 GrowthBook / env / build flag 的存在写成“当前版本一定对外可用”

这里会做的事：

- 按主题归纳 `feature(...)`、GrowthBook、env flag、条件注入分支
- 给出关键源码路径
- 区分“源码能确认的行为”和“不能确认的上线状态”
- 提醒哪些名字容易被误写成完整产品能力

## 阅读顺序

1. [runtime-and-prompt-gates.md](./runtime-and-prompt-gates.md)
2. [agent-memory-compact-gates.md](./agent-memory-compact-gates.md)
3. [remote-bridge-and-session-gates.md](./remote-bridge-and-session-gates.md)

## 先记住的边界

- `feature(...)` 更接近编译期 tree-shaking 边界，不等于“当前二进制一定开启”。
- `getFeatureValue_CACHED_MAY_BE_STALE(...)` / `getDynamicConfig_*` 说明有运行时 gate，不等于“该能力已经公开发布”。
- `process.env.*` 说明有环境变量控制面，不等于“普通用户一定能看到这个入口”。

## 高风险误写点

- `KAIROS`、`PROACTIVE`、`COORDINATOR_MODE`：当前更适合写成 prompt / runtime 分支，不适合直接写成公开产品模式。
- `BUDDY`、`VOICE_MODE`：当前能确认 companion / voice 的代码接线与 gate，但不能外推完整产品闭环。
- `BRIDGE_MODE`、`tengu_ccr_bridge`、`tengu_bridge_repl_v2`：当前能确认本地桥接与远端控制路径存在，但不能把服务端形态写死。
- `CONTEXT_COLLAPSE`、`REACTIVE_COMPACT`：当前能确认 query loop 有对应分支，但不能把它们写成所有构建里的默认 compact 策略。
