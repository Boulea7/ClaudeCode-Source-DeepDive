[简体中文](./README.md) | [English](./README.en.md) | [繁體中文](./README.zh-TW.md) | [日本語](./README.ja.md)

# Claude Code Source Deep Dive

一個圍繞 `Claude Code` 公開鏡像原始碼建立的非官方研究倉庫。

這份倉庫主要回答一類問題：`main.tsx` 分出的兩個入口路徑，怎樣匯入共享的 `query/runtime` 主鏈，以及 tools、MCP、skills、plugins、permissions、memory、compact、tasks、prompts 等系統怎樣掛到這條主鏈上。

詳細文件目前以簡體中文與英文為主；本頁提供導覽與摘要，方便先建立整體地圖。

## 你可以在這裡確認什麼

- 互動式路徑怎樣從 `main.tsx` 進入 `launchRepl()`、`REPL.tsx`，再進入 `query()`
- 非互動 / SDK 路徑怎樣從 `main.tsx` 進入 `QueryEngine.ts`，再進入 `query()`
- `Tool.ts` 與 `tools.ts` 怎樣定義工具協議、內建工具集合、MCP 合併後的工具池
- `query.ts` 怎樣處理工具執行、attachments、compact、stop hooks、續跑條件與跨回合刷新
- 哪些結論已有原始碼支撐，哪些名稱與分支仍需保守書寫

## 從哪裡開始讀

| 目標 | 建議入口 | 你會得到什麼 |
| --- | --- | --- |
| 先建立整體地圖 | [ARCHITECTURE.en.md](./ARCHITECTURE.en.md) | 兩個入口路徑、共享主鏈、關鍵入口檔案 |
| 按子系統閱讀 | [MODULES/README.en.md](./MODULES/README.en.md) | 8 個模組的總覽、簡單版、深讀版入口 |
| 只看 prompt 裝配 | [PROMPTS/README.en.md](./PROMPTS/README.en.md) | system prompt、agent prompt、skill 注入路徑 |
| 只看 gated 分支 | [FEATURE-FLAGS/README.en.md](./FEATURE-FLAGS/README.en.md) | 編譯期 gate、執行期 gate、條件路徑線索 |
| 快速瀏覽全倉 | [SIMPLE/README.en.md](./SIMPLE/README.en.md) | 面向第一次進入倉庫的短路線 |
| 直接進入深讀 | [DEEP/README.en.md](./DEEP/README.en.md) | 面向原始碼追讀的長路線 |

## 閱讀路線

### 路線 A：先看整體圖

1. [ARCHITECTURE.md](./ARCHITECTURE.md)
2. [MODULES/README.en.md](./MODULES/README.en.md)
3. 任一模組的 `README.en.md`
4. 任一模組的 `SIMPLE/README.en.md`
5. 任一模組的 `DEEP/README.en.md`

### 路線 B：先追共享主鏈

1. [ARCHITECTURE.en.md](./ARCHITECTURE.en.md)
2. [01-agent-loop-and-teams/README.en.md](./MODULES/01-agent-loop-and-teams/README.en.md)
3. [02-planning-compaction-and-assistant/README.en.md](./MODULES/02-planning-compaction-and-assistant/README.en.md)
4. [03-persistent-memory-system/README.en.md](./MODULES/03-persistent-memory-system/README.en.md)
5. [05-tools-mcp-skills-and-plugins/README.en.md](./MODULES/05-tools-mcp-skills-and-plugins/README.en.md)
6. [06-permissions-sandbox-and-trust/README.en.md](./MODULES/06-permissions-sandbox-and-trust/README.en.md)

### 路線 C：先看 prompts、gate 與遠端路徑

1. [PROMPTS/README.en.md](./PROMPTS/README.en.md)
2. [FEATURE-FLAGS/README.en.md](./FEATURE-FLAGS/README.en.md)
3. [07-remote-session-bridge-and-sdk/README.en.md](./MODULES/07-remote-session-bridge-and-sdk/README.en.md)
4. [08-prompts-config-and-other-moats/README.en.md](./MODULES/08-prompts-config-and-other-moats/README.en.md)

## 主要文件與目錄

```text
.
├── README.md
├── README.en.md
├── README.zh-TW.md
├── README.ja.md
├── ARCHITECTURE.md
├── ARCHITECTURE.en.md
├── DISCLAIMER.md
├── DISCLAIMER.en.md
├── MODULES/
├── PROMPTS/
├── FEATURE-FLAGS/
├── SIMPLE/
├── DEEP/
├── COMPARISONS/
├── EXAMPLES/
├── ASSETS/
└── AI-AGENT/
```

首次閱讀建議先看 `README`、`ARCHITECTURE`、`MODULES`、`PROMPTS`、`FEATURE-FLAGS`。`AI-AGENT/` 提供面向自動化閱讀的結構化補充材料。

## 閱讀邊界

- 這是非官方研究倉庫
- 原始碼事實邊界是公開鏡像 `ChinaSiro/claude-code-sourcemap` 與本地 `_upstream/claude-code-sourcemap/`
- `feature()`、GrowthBook、env gate 說明條件路徑存在，這些線索本身不足以說明公開 rollout
- `Buddy`、`KAIROS`、`PROACTIVE`、`voice`、`bridge`、`remote isolation` 等名稱保持原始碼字面和上下文範圍

完整邊界說明見 [DISCLAIMER.md](./DISCLAIMER.md)。

## 繼續閱讀

- [MODULES/README.en.md](./MODULES/README.en.md)
- [PROMPTS/README.en.md](./PROMPTS/README.en.md)
- [FEATURE-FLAGS/README.en.md](./FEATURE-FLAGS/README.en.md)
- [COMPARISONS/README.en.md](./COMPARISONS/README.en.md)
- [EXAMPLES/README.en.md](./EXAMPLES/README.en.md)
- [ASSETS/README.en.md](./ASSETS/README.en.md)
- [CONTRIBUTING.md](./CONTRIBUTING.md) / [CONTRIBUTING.en.md](./CONTRIBUTING.en.md)
- [SECURITY.md](./SECURITY.md) / [SECURITY.en.md](./SECURITY.en.md)
- [AI-AGENT](./AI-AGENT/)：面向自動化閱讀的結構化補充材料
