[简体中文](./system-prompt-sections.md) | [English](./system-prompt-sections.en.md)

# System Prompt Sections

这一页只解释 section registry，不解释每个 raw section 的正文。

## 关键源码文件

- `_upstream/claude-code-sourcemap/restored-src/src/constants/systemPromptSections.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/constants/prompts.ts`
- `_upstream/claude-code-sourcemap/restored-src/src/utils/sessionRestore.ts`

## 当前源码能确认的机制

- `systemPromptSection(name, compute)` 创建可缓存 section。
- `DANGEROUS_uncachedSystemPromptSection(name, compute, reason)` 创建逐轮重算 section。
- `resolveSystemPromptSections()` 会：
  - 命中 cache 时直接返回缓存值
  - 未命中时执行 `compute()`
  - 把结果写回 cache
- `clearSystemPromptSections()` 会清空 section cache，并重置 beta header latches。
- 源码注释明确写明 section cache 会在 `/clear` 与 `/compact` 相关路径后重置。
- `prompts.ts` 当前注册的主要 section 名包括：
  - `session_guidance`
  - `memory`
  - `ant_model_override`
  - `env_info_simple`
  - `language`
  - `output_style`
  - `mcp_instructions`
  - `scratchpad`
  - `frc`
  - `summarize_tool_results`
  - `numeric_length_anchors`
  - `token_budget`
  - `brief`
- `mcp_instructions` 是显式的 `DANGEROUS_uncachedSystemPromptSection()`。

## 当前源码不能确认的内容

- 某个 section 在公开构建里的默认启用状态。
- 某个 section 的运行时最终正文。

## 复核清单

- 是否把 section cache 写成永久缓存。
- 是否漏写 `/clear`、`/compact` 相关重置语义。
- 是否把 `mcp_instructions` 误写成普通缓存 section。
