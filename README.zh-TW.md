[简体中文](./README.md) | [English](./README.en.md) | [繁體中文](./README.zh-TW.md) | [日本語](./README.ja.md)

# Claude Code Source Deep Dive

一個以原始碼拆解為核心的 `Claude Code` 非官方研究倉庫。

這個倉庫固定聚焦三件事：

- 執行鏈如何接起來
- 模組之間如何分層
- 哪些結論已有原始碼支撐，哪些地方仍需保守描述

## 你可以在這裡確認什麼

- 互動式主執行緒如何從 `main.tsx` 進入 `REPL.tsx`，再進入 `query.ts`
- `QueryEngine.ts` 在非互動 / SDK 路徑中扮演什麼角色
- tools、MCP、skills、plugins、permissions、memory、compact、tasks 如何接到同一條執行鏈上
- prompt 裝配、feature gate、remote / bridge 相關程式碼目前能確認到什麼程度

## 這個倉庫如何使用原始碼

- 程式碼事實只來自：
  - `https://github.com/ChinaSiro/claude-code-sourcemap`
  - 本地鏡像：`_upstream/claude-code-sourcemap/`
- 本倉庫引用的原始碼路徑，預設指向目前倉庫裡真實存在的：
  - `_upstream/claude-code-sourcemap/restored-src/src/...`

完整邊界說明見 [DISCLAIMER.md](./DISCLAIMER.md) 與 [DISCLAIMER.en.md](./DISCLAIMER.en.md)。

## 從哪裡開始讀

| 目標 | 建議入口 | 你會得到什麼 |
| --- | --- | --- |
| 先建立整體地圖 | [ARCHITECTURE.md](./ARCHITECTURE.md) | 主執行鏈、分層關係、關鍵入口檔案 |
| 按模組系統閱讀 | [MODULES/README.md](./MODULES/README.md) | 8 個模組的總覽、簡單版、深讀版入口 |
| 只看 prompt 裝配 | [PROMPTS/README.md](./PROMPTS/README.md) | system prompt、agent prompt、skill 注入路徑 |
| 只看 gated 分支 | [FEATURE-FLAGS/README.md](./FEATURE-FLAGS/README.md) | 編譯期 gate、執行期 gate、隱藏能力線索 |
| 快速瀏覽全倉 | [SIMPLE/README.md](./SIMPLE/README.md) | 給第一次進入倉庫的短路線 |
| 直接進入深讀 | [DEEP/README.md](./DEEP/README.md) | 給原始碼追讀的長路線 |

## 閱讀路線

### 路線 A：先看整張圖

1. [ARCHITECTURE.md](./ARCHITECTURE.md)
2. [MODULES/README.md](./MODULES/README.md)
3. 任一模組的 `SIMPLE/README.md`
4. 任一模組的 `DEEP/README.md`

### 路線 B：先追主執行鏈

1. [ARCHITECTURE.md](./ARCHITECTURE.md)
2. [MODULES/01-agent-loop-and-teams](./MODULES/01-agent-loop-and-teams/)
3. [MODULES/02-planning-compaction-and-assistant](./MODULES/02-planning-compaction-and-assistant/)
4. [MODULES/03-persistent-memory-system](./MODULES/03-persistent-memory-system/)
5. [MODULES/05-tools-mcp-skills-and-plugins](./MODULES/05-tools-mcp-skills-and-plugins/)
6. [MODULES/06-permissions-sandbox-and-trust](./MODULES/06-permissions-sandbox-and-trust/)

### 路線 C：先看 prompt、gate 與隱藏分支

1. [PROMPTS/README.md](./PROMPTS/README.md)
2. [FEATURE-FLAGS/README.md](./FEATURE-FLAGS/README.md)
3. [MODULES/08-prompts-config-and-other-moats](./MODULES/08-prompts-config-and-other-moats/)
4. [MODULES/07-remote-session-bridge-and-sdk](./MODULES/07-remote-session-bridge-and-sdk/)

## 倉庫結構

```text
.
├── README.md
├── README.en.md
├── README.zh-TW.md
├── README.ja.md
├── DISCLAIMER.md
├── ARCHITECTURE.md
├── SIMPLE/
├── DEEP/
├── MODULES/
├── PROMPTS/
├── FEATURE-FLAGS/
├── COMPARISONS/
├── EXAMPLES/
└── ASSETS/
```

## 閱讀時需要記住的邊界

- 這是非官方研究倉庫，不代表 Anthropic 官方結構、發布計畫或產品口徑
- `feature()`、GrowthBook、env gate 只能說明程式碼裡存在條件分支，不能直接說明公開 rollout
- `Buddy`、`KAIROS`、`PROACTIVE`、`voice`、`bridge`、`remote isolation` 等名稱只按原始碼證據保守書寫
- `SYSTEM_PROMPT_DYNAMIC_BOUNDARY`、`mcp_instructions` 等 prompt 片段都要按條件路徑理解，不能寫成固定常駐段落

## 繼續閱讀

- [MODULES/README.md](./MODULES/README.md)
- [PROMPTS/README.md](./PROMPTS/README.md)
- [FEATURE-FLAGS/README.md](./FEATURE-FLAGS/README.md)
- [COMPARISONS/README.md](./COMPARISONS/README.md)
- [EXAMPLES/README.md](./EXAMPLES/README.md)

## 機器可讀索引

如果你要給其他 agent 餵結構化材料，可以再看：

- [AI-AGENT](./AI-AGENT/)
