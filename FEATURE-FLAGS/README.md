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

- `KAIROS`
  - 当前源码能证明：它会改写 prompt、assistant / brief、memory daily-log 等分支。
  - 当前不能证明：它在公开构建里等同于某个固定产品模式。
  - 推荐写法：`KAIROS` 是会影响 prompt / runtime / memory 的 gated branch。
- `PROACTIVE`
  - 当前源码能证明：它会改变 main-thread agent prompt 与默认 prompt 的拼接方式。
  - 当前不能证明：它已经固定等同于公开 autonomous mode。
  - 推荐写法：`PROACTIVE` 是 prompt / runtime 分支，不是发布状态说明。
- `Buddy`
  - 当前源码能证明：companion sprite、notification、intro attachment 与 reaction callback 路径存在。
  - 当前不能证明：observer 生成机制、pet 写入路径、正式产品命名。
  - 推荐写法：`Buddy` 是 gated companion / watcher 线索。
- `voice`
  - 当前源码能证明：开关、预检、本地录音、STT、输入框回填。
  - 当前不能证明：TTS、playback、双向语音产品闭环。
  - 推荐写法：`voice` 当前更像 feature-gated 的语音听写增强链路。
- `remote isolation`
  - 当前源码能证明：`remote/` 与 `bridge/` 有分层，且有 env-based / env-less / compat 分支。
  - 当前不能证明：服务端真实隔离形态与默认部署策略。
  - 推荐写法：只写客户端预期、桥接方式与 compat 逻辑。
- `bridge`
  - 当前源码能证明：本地出站桥接、transport、worker、session compat 路径存在。
  - 当前不能证明：它是一个公开本地服务端产品面。
  - 推荐写法：`bridge` 是本地到远端控制面的出站桥接层。
- `Chicago MCP`
  - 当前源码能证明：Computer Use / Chicago MCP 相关路径受 gate 控制。
  - 当前不能证明：它已对所有用户公开或默认启用。
  - 推荐写法：只写成 gated branch 或 hidden capability clue。
- `TEAMMEM`
  - 当前源码能证明：team subtree、path validation、部分 prompt / extract 分支存在。
  - 当前不能证明：所有用户默认都有 team memory，或所有写链都统一走同一入口。
  - 推荐写法：`TEAMMEM` 是 auto memory 根下的 gated team branch。
