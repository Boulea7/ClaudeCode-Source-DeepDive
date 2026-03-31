# System Prompt Sections

这一页只讲 section 机制本身。

也就是：

**Claude Code 怎么把动态 prompt 段注册、缓存、失效，再重新求值。**

## 关键文件

- `restored-src/src/constants/systemPromptSections.ts`
- `restored-src/src/constants/prompts.ts`

## 先看三件核心对象

`systemPromptSections.ts` 里只有三件真正关键的东西：

- `systemPromptSection(name, compute)`
  - 普通 section，会缓存
- `DANGEROUS_uncachedSystemPromptSection(name, compute, reason)`
  - 每轮重算的 volatile section
- `resolveSystemPromptSections(sections)`
  - 把注册好的 section 真正求值成 prompt 字符串数组

这里最重要的字段就是：

- `cacheBreak`

它直接决定这个 section 是：

- 可复用
- 还是每轮都要重新算

## 普通 section 与 uncached section 的区别

`systemPromptSection()`：

- `cacheBreak: false`
- 如果 cache 里已有同名项，就直接复用

`DANGEROUS_uncachedSystemPromptSection()`：

- `cacheBreak: true`
- 每轮都重新执行 `compute`
- 然后再把最新值写回 cache

也就是说，uncached 不是“完全不进 cache”，而是“不允许用旧 cache 命中直接返回”。

## `resolveSystemPromptSections()` 的行为很简单，但很重要

`resolveSystemPromptSections()` 会：

1. 读取当前 section cache
2. 逐个 section 看 `cacheBreak`
3. 如果是普通 section 且 cache 命中，就直接返回
4. 否则执行 `compute`
5. 用 `setSystemPromptSectionCacheEntry()` 写回最新值

这让 prompt section 更像一个 registry，而不是 scattered string builder。

## `clearSystemPromptSections()` 会在 `/clear` 和 `/compact` 后失效缓存

`clearSystemPromptSections()` 做了两件事：

- `clearSystemPromptSectionState()`
- `clearBetaHeaderLatches()`

源码注释也写得很清楚：

- 它会在 `/clear`
- 以及 `/compact`

后调用。

所以 compact 不只是重写消息历史，也会让 section cache 重新求值。

## 为什么 `mcp_instructions` 是显式 uncached

这是当前 section 机制里最值得单独拿出来讲的例子。

在 `prompts.ts` 里：

- `mcp_instructions`
- 用的是 `DANGEROUS_uncachedSystemPromptSection(...)`

原因源码里已经直接写出来了：

- MCP servers 可能在 turn 之间连接或断开

这意味着：

- 如果把它放进普通缓存
- prompt cache 会更稳定
- 但模型看到的 MCP instructions 就可能过期

所以作者在这里明确选择了“动态正确性优先”。

## 为什么 `session_guidance` 也必须放在动态边界之后

`session_guidance` 依赖的不是固定文本，而是运行时条件，例如：

- 当前是不是 non-interactive session
- fork gate 是否开启

因此它也不应该混进静态前缀。

更准确地说，当前默认 prompt parts 的静态/动态边界不是审美问题，而是缓存边界设计。

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

## 为什么 section 机制重要

如果没有这层 registry，prompt 装配会面临两个问题：

- 不是每轮都知道哪些段是真动态的
- compact / clear 后也不知道该让哪些段失效

现在这套机制至少带来了三点好处：

- 动态段可以按名管理
- cache break 是显式语义，不靠注释猜
- `/clear` 和 `/compact` 的失效边界清楚

## 已确认的事实

- section 在源码里是一等结构，不是文档概念
- 普通 section 会命中 cache
- uncached section 每轮重算
- `/clear` 和 `/compact` 会清 section cache
- `mcp_instructions` 是显式 uncached section
- `session_guidance` 属于动态段，而不是静态前缀

## 仍待确认

- 某些 feature gate 在不同构建里是否会增减 section 集合
- beta header latches 在完整产品里的影响范围，这一页不展开
