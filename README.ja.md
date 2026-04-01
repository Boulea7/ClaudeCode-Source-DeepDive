[简体中文](./README.md) | [English](./README.en.md) | [繁體中文](./README.zh-TW.md) | [日本語](./README.ja.md)

# Claude Code Source Deep Dive

`Claude Code` をソースコード中心で読み解くための非公式リサーチリポジトリです。

このリポジトリは次の 3 点に集中します。

- 実行チェーンがどうつながるか
- モジュールがどう分かれているか
- どこまでがソースで確認でき、どこから先は慎重な表現が必要か

## ここで確認できること

- 対話型メインスレッドが `main.tsx` から `REPL.tsx` を経て `query.ts` に入る流れ
- `QueryEngine.ts` が非対話 / SDK 経路で担う役割
- tools、MCP、skills、plugins、permissions、memory、compact、tasks が同じ実行チェーンにどう接続されるか
- prompt assembly、feature gate、remote / bridge 関連コードをどこまで確認できるか

## このリポジトリのソース利用方針

- コード上の事実は次の 2 つだけを根拠にしています。
  - `https://github.com/ChinaSiro/claude-code-sourcemap`
  - ローカルミラー：`_upstream/claude-code-sourcemap/`
- このリポジトリで引用するソースパスは、実際に存在する次の場所を指します。
  - `_upstream/claude-code-sourcemap/restored-src/src/...`

詳細な境界は [DISCLAIMER.md](./DISCLAIMER.md) と [DISCLAIMER.en.md](./DISCLAIMER.en.md) を参照してください。

## 読み始める場所

| 目的 | 入口 | 得られるもの |
| --- | --- | --- |
| まず全体像をつかむ | [ARCHITECTURE.md](./ARCHITECTURE.md) | 実行チェーン、主要レイヤー、重要な入口ファイル |
| モジュールごとに読む | [MODULES/README.md](./MODULES/README.md) | 8 モジュールの概要、簡易版、詳細版への入口 |
| prompt assembly を見る | [PROMPTS/README.md](./PROMPTS/README.md) | system prompt、agent prompt、skill injection の経路 |
| gated branch を見る | [FEATURE-FLAGS/README.md](./FEATURE-FLAGS/README.md) | コンパイル時 gate、実行時 gate、hidden capability の手がかり |
| リポジトリを手早く回る | [SIMPLE/README.md](./SIMPLE/README.md) | 初見向けの短い読み方 |
| そのまま深掘りする | [DEEP/README.md](./DEEP/README.md) | ソース追跡向けの長い読み方 |

## 読み方の例

### ルート A：まず地図を作る

1. [ARCHITECTURE.md](./ARCHITECTURE.md)
2. [MODULES/README.md](./MODULES/README.md)
3. 任意のモジュールの `SIMPLE/README.md`
4. 任意のモジュールの `DEEP/README.md`

### ルート B：実行チェーンから追う

1. [ARCHITECTURE.md](./ARCHITECTURE.md)
2. [MODULES/01-agent-loop-and-teams](./MODULES/01-agent-loop-and-teams/)
3. [MODULES/02-planning-compaction-and-assistant](./MODULES/02-planning-compaction-and-assistant/)
4. [MODULES/03-persistent-memory-system](./MODULES/03-persistent-memory-system/)
5. [MODULES/05-tools-mcp-skills-and-plugins](./MODULES/05-tools-mcp-skills-and-plugins/)
6. [MODULES/06-permissions-sandbox-and-trust](./MODULES/06-permissions-sandbox-and-trust/)

### ルート C：prompt、gate、hidden branch から入る

1. [PROMPTS/README.md](./PROMPTS/README.md)
2. [FEATURE-FLAGS/README.md](./FEATURE-FLAGS/README.md)
3. [MODULES/08-prompts-config-and-other-moats](./MODULES/08-prompts-config-and-other-moats/)
4. [MODULES/07-remote-session-bridge-and-sdk](./MODULES/07-remote-session-bridge-and-sdk/)

## リポジトリ構成

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

## 読むときに保持すべき境界

- これは非公式の研究リポジトリです。Anthropic の公式構造、公開計画、製品表現を代表しません。
- `feature()`、GrowthBook、env gate は条件分岐の存在を示すだけで、公開 rollout を証明しません。
- `Buddy`、`KAIROS`、`PROACTIVE`、`voice`、`bridge`、`remote isolation` などの名称は、ソースで確認できる範囲に限定して慎重に扱います。
- `SYSTEM_PROMPT_DYNAMIC_BOUNDARY` や `mcp_instructions` のような prompt 断片は、常駐セクションではなく条件付きの経路要素として理解する必要があります。

## 続けて読む

- [MODULES/README.md](./MODULES/README.md)
- [PROMPTS/README.md](./PROMPTS/README.md)
- [FEATURE-FLAGS/README.md](./FEATURE-FLAGS/README.md)
- [COMPARISONS/README.md](./COMPARISONS/README.md)
- [EXAMPLES/README.md](./EXAMPLES/README.md)

## 機械可読インデックス

他の agent に構造化資料を渡したい場合は、次も参照できます。

- [AI-AGENT](./AI-AGENT/)
