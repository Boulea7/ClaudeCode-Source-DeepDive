[简体中文](./ARCHITECTURE.md) | [English](./ARCHITECTURE.en.md)

# Claude Code 全局架构总览

这一页给出一张可追源码的总图。

当前公开镜像显示：`main.tsx` 分出两个主要入口路径，它们都会汇入共享的 `query/runtime` 主链。

## 两个入口路径与共享主链

- 交互式主线程：
  - `main.tsx -> launchRepl() -> REPL.tsx -> query()`
- 非交互 / SDK 路径：
  - `main.tsx -> QueryEngine.ts -> query()`

这两条路径共享的核心运行面包括：

- tool pool
- prompt assembly 与上下文装配
- permissions 与 approvals
- memory 与 compaction
- tasks 与 agent runtime
- MCP、skills、plugins
- attachments、stop hooks、续跑条件

## 关键入口文件

当前仓库里可直接复核的源码路径位于：

- `_upstream/claude-code-sourcemap/restored-src/src/main.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/screens/REPL.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/QueryEngine.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/query.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/Tool.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools.ts`

## 一张图看总链

```mermaid
flowchart LR
    A[main.tsx] --> B{entry path}
    B --> C[launchRepl()]
    B --> D[QueryEngine.ts]
    C --> E[REPL.tsx]
    E --> G[query()]
    D --> G
    G --> H[tool execution and attachments]
    G --> I[memory and compaction]
    G --> J[permissions and approvals]
    G --> K[tasks and agent runtime]
    E --> L[prompt assembly and interactive context]
    D --> M[prompt assembly and transcript state]
    E --> N[tool pool and MCP merge]
```

## 这些层分别在做什么

### 启动与装配

`main.tsx` 负责 CLI 启动、配置与模型准备、permission context、MCP 相关初始化，以及 bundled plugins / skills 的注册。交互式会话随后进入 `launchRepl()`；headless / SDK 场景走 `QueryEngine.ts` 这条包装路径。

### 交互式编排层

`REPL.tsx` 是交互式路径的核心编排层。源码里它会从当前 store 读取 fresh tools 与 MCP clients，组装 effective system prompt，并直接 `for await ... of query(...)` 驱动共享 query loop。把它写成纯展示层会丢掉关键事实。

### 非交互 / SDK 包装层

`QueryEngine.ts` 也是围绕 `query(...)` 的包装层。它负责整理消息状态、prompt parts、transcript / structured IO 相关处理，再以 `querySource: 'sdk'` 进入同一条共享 query loop。

### 共享 query loop

`query.ts` 是共享的 turn execution core。这里维护循环状态，处理 tool execution、attachment 注入、compact、stop hooks、继续条件，并在跨回合时刷新工具集合与上下文。

### 工具协议与工具池

`Tool.ts` 定义统一的工具协议与 `ToolUseContext`。`tools.ts` 负责具体工具池装配：`getTools()` 处理内建工具与过滤规则，`assembleToolPool()` 负责把内建工具与 MCP 工具合并成一致的运行时工具池。

## 阅读这张图时要保留的边界

- `REPL.tsx` 与 `QueryEngine.ts` 都会进入同一个 `query()`，它们承担的入口职责不同
- `ToolUseContext` 同时携带运行态与部分 REPL UI 字段，文档写法需要区分 UI-only 状态与 API / transcript 状态
- tool pool 会受 deny rules、agent 限制、feature gate、运行时状态与 MCP 连接状态影响
- `SYSTEM_PROMPT_DYNAMIC_BOUNDARY`、`mcp_instructions` 等 prompt 片段要按条件路径理解
- `Buddy`、`KAIROS`、`voice`、`bridge`、remote 相关名称保持源码字面和上下文范围

## 下一步看哪里

- 想按模块继续读：
  - [MODULES/README.md](./MODULES/README.md)
- 想单独看 prompt 装配：
  - [PROMPTS/README.md](./PROMPTS/README.md)
- 想单独看 gate：
  - [FEATURE-FLAGS/README.md](./FEATURE-FLAGS/README.md)
