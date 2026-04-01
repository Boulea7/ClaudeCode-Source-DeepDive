[简体中文](./system-prompt-source-index.md) | [English](./system-prompt-source-index.en.md)

# System Prompt Source Index

这一页只做索引与检查，不做 raw system prompt 全量转储。

## 这页负责什么

- 列出 system prompt 的主要来源文件
- 区分 interactive、non-interactive、ordinary subagent、fork subagent 几条路径
- 列出会改写 prompt 的关键 section、gate 和 attachment
- 提供复核时的检查清单

## 主来源文件

- `_upstream/claude-code-sourcemap/restored-src/src/constants/prompts.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/constants/systemPromptSections.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/systemPrompt.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/queryContext.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/screens/REPL.tsx`
- `_upstream/claude-code-sourcemap/restored-src/src/QueryEngine.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/runAgent.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/tools/AgentTool/forkSubagent.ts`

## 按路径查看

### 1. default prompt parts

- 来源：
  - `constants/prompts.ts -> getSystemPrompt()`
- 需要检查：
  - simple path
  - standard path
  - proactive / KAIROS path
  - `SYSTEM_PROMPT_DYNAMIC_BOUNDARY` 是否条件插入

### 2. interactive main thread

- 来源：
  - `screens/REPL.tsx`
  - `utils/systemPrompt.ts -> buildEffectiveSystemPrompt()`
- 需要检查：
  - `getSystemPrompt()`
  - `getUserContext()`
  - `getSystemContext()`
  - `buildEffectiveSystemPrompt()`
  - `toolUseContext.renderedSystemPrompt`

### 3. non-interactive main thread

- 来源：
  - `utils/queryContext.ts`
  - `QueryEngine.ts`
- 需要检查：
  - `fetchSystemPromptParts()`
  - `customSystemPrompt`
  - `appendSystemPrompt`
  - `memoryMechanicsPrompt`
  - `customSystemPrompt` 存在时是否跳过默认预取

### 4. ordinary subagent

- 来源：
  - `tools/AgentTool/runAgent.ts`
- 需要检查：
  - `agentDefinition.getSystemPrompt()`
  - `enhanceSystemPromptWithEnvDetails()`
  - `DEFAULT_AGENT_PROMPT` fallback

### 5. fork subagent

- 来源：
  - `tools/AgentTool/forkSubagent.ts`
  - `tools/AgentTool/runAgent.ts`
- 需要检查：
  - `renderedSystemPrompt`
  - 精确工具池
  - `thinkingConfig`
  - `buildForkedMessages()`
  - gate 条件与 fallback

## 重点 section 与条件项

- `SYSTEM_PROMPT_DYNAMIC_BOUNDARY`
- `mcp_instructions`
- `session_guidance`
- `output_style`
- `language`
- `memory`
- `env_info_simple`

## 检查清单

- `SYSTEM_PROMPT_DYNAMIC_BOUNDARY` 是否按条件插入
- `mcp_instructions` 是否走 inline section 还是 delta / attachment
- interactive 与 non-interactive 是否被写成了同一条链
- ordinary subagent 与 fork subagent 是否被混写
- `Buddy`、`KAIROS`、`PROACTIVE`、`COORDINATOR_MODE` 是否被写成公开固定模式
- 是否误把整份 raw system prompt 复制进文档

## 保守边界

- 这一页只做来源索引，不贴大段 raw system prompt
- feature gate 只说明代码分支，不说明 rollout
- 某条 prompt 路径存在，不说明所有构建都会走到
