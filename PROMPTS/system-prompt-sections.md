# System Prompt Sections

这一页只讲 section 机制本身。

也就是：

**Claude Code 怎么把动态 prompt 段注册、缓存、失效，再重新求值。**

## 这部分负责什么

这一页主要解释四件事：

1. section 是怎么注册的
2. cacheBreak / uncached 是什么语义
3. `resolveSystemPromptSections()` 怎么求值
4. `/clear` 与 `/compact` 为什么会影响 section cache

## 关键文件

- `restored-src/src/constants/systemPromptSections.ts`
- `restored-src/src/constants/prompts.ts`

## 执行流

### 1. section 在源码里是一等结构

`systemPromptSections.ts` 里最关键的三个对象是：

- `systemPromptSection(name, compute)`
- `DANGEROUS_uncachedSystemPromptSection(name, compute, reason)`
- `resolveSystemPromptSections(sections)`

这说明 dynamic prompt 不是 scattered string builder，而是有注册表语义的一等结构。

### 2. `cacheBreak` 决定 section 的缓存语义

普通 section：

- `cacheBreak: false`

uncached section：

- `cacheBreak: true`

对应到两个 helper：

- `systemPromptSection()`
  - 命中 cache 时直接复用
- `DANGEROUS_uncachedSystemPromptSection()`
  - 每轮都重新执行 `compute()`

这里有一个需要写清的细节：

- uncached 不等于“完全不写 cache”
- 它的真实语义是“不能用旧 cache 命中直接返回”

也就是说，uncached section 仍会把最新值写回缓存槽位，只是下一轮不会直接拿旧值跳过计算。

### 3. `resolveSystemPromptSections()` 负责真正求值

`resolveSystemPromptSections()` 的行为很简单，但很重要：

1. 读取当前 section cache
2. 逐个 section 看 `cacheBreak`
3. 普通 section 且 cache 命中时直接复用
4. 否则执行 `compute()`
5. 把最新值写回 cache

这也是为什么 section cache 更像：

- “按 section name 的注册表缓存”

而不是：

- “整段 system prompt 的一次性缓存”

### 4. `clearSystemPromptSections()` 会在 `/clear` 和 `/compact` 后失效

`clearSystemPromptSections()` 做了两件事：

- `clearSystemPromptSectionState()`
- `clearBetaHeaderLatches()`

源码注释也明确说明：

- `/clear` 会调用它
- `/compact` 也会调用它

所以 compact 不只是重写消息历史，还会让 section cache 重新求值。

### 5. `mcp_instructions` 是当前最明确的 uncached section

这轮重新核读后，这一点可以写得更强一些。

当前标准路径里，明确使用：

- `DANGEROUS_uncachedSystemPromptSection(...)`

的 section 是：

- `mcp_instructions`

原因也直接写在源码注释里：

- MCP servers 可能在 turn 之间连接或断开

这意味着作者在这里明确选择了：

- 动态正确性优先

而不是：

- 缓存稳定性优先

### 6. static boundary / dynamic boundary 不是审美问题

`SYSTEM_PROMPT_DYNAMIC_BOUNDARY` 的作用不是“看起来更整齐”，而是把：

- 跨组织可缓存的静态内容
- 用户 / 会话 / 运行时相关的动态内容

明确切开。

当前标准路径里：

- boundary 之前是静态块
- boundary 之后是 `resolvedDynamicSections`
- 但这条 boundary 是按条件插入的，不是每次必有

像下面这些段落，应该理解成 dynamic side：

- `session_guidance`
- `memory`
- `env_info_simple`
- `language`
- `output_style`
- `mcp_instructions`

所以这一页要把几个词统一好：

- static sections
- dynamic sections
- dynamic boundary
- cacheBreak

## 一张图看 section 生命周期

```mermaid
flowchart TD
    A[register section] --> B{cacheBreak?}
    B -- no --> C[check cache by name]
    C -- hit --> D[reuse cached value]
    C -- miss --> E[compute]
    B -- yes --> E
    E --> F[write latest value into cache]
    F --> G[resolved prompt part]
    H[/clear or /compact] --> I[clearSystemPromptSections]
    I --> J[clear section state and beta latches]
```

## 为什么这个设计重要

如果没有这层 section registry，prompt 装配会面临两个问题：

- 不知道哪些段是真动态的
- `/clear` 与 `/compact` 之后也不知道哪些值该失效

现在这套机制至少带来了三点好处：

- 动态段可以按名管理
- `cacheBreak` 是显式语义，不靠注释猜
- `/clear` 与 `/compact` 的失效边界清楚
- boundary 是否出现，取决于当前路径是否启用全局缓存边界

## 推荐阅读顺序

1. `restored-src/src/constants/systemPromptSections.ts`
2. `restored-src/src/constants/prompts.ts`
3. `restored-src/src/utils/systemPrompt.ts`
4. `restored-src/src/utils/queryContext.ts`

## 仍待确认

- 某些 feature gate 会不会在不同构建里增减 section 集合，这一页不展开。
- `beta header latches` 的完整产品语义，这一页也不继续延伸。
