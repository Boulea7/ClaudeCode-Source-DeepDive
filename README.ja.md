[简体中文](./README.md) | [English](./README.en.md) | [繁體中文](./README.zh-TW.md) | [日本語](./README.ja.md)

# Claude Code Source Deep Dive

`Claude Code` の公開ソースミラーを起点に読み解く非公式リサーチリポジトリです。

このリポジトリが主に扱うのは、`main.tsx` から分岐する 2 つの入口経路がどのように共有の `query/runtime` 主線へ合流するか、そして tools、MCP、skills、plugins、permissions、memory、compact、tasks、prompts などの各システムがその主線にどう接続されるかです。

詳細ドキュメントは主に簡体字中国語版と英語版です。このページは概要と導線をまとめた案内ページです。

## ここで確認できること

- 対話型経路が `main.tsx` から `launchRepl()`、`REPL.tsx` を経て `query()` に入る流れ
- 非対話 / SDK 経路が `main.tsx` から `QueryEngine.ts` を経て `query()` に入る流れ
- `Tool.ts` と `tools.ts` がツール契約、組み込みツール集合、MCP 統合後のツールプールをどう定義するか
- `query.ts` がツール実行、attachments、compact、stop hooks、継続条件、ターン間の再読込をどう扱うか
- どこまでがソースで確認済みで、どの名称や分岐に慎重な表現が必要か

## 読み始める場所

| 目的 | 入口 | 得られるもの |
| --- | --- | --- |
| まず全体像をつかむ | [ARCHITECTURE.en.md](./ARCHITECTURE.en.md) | 2 つの入口経路、共有主線、主要な入口ファイル |
| サブシステムごとに読む | [MODULES/README.en.md](./MODULES/README.en.md) | 8 モジュールの概要、簡易版、詳細版への入口 |
| prompt assembly を追う | [PROMPTS/README.en.md](./PROMPTS/README.en.md) | system prompt、agent prompt、skill injection の経路 |
| gated branch を追う | [FEATURE-FLAGS/README.en.md](./FEATURE-FLAGS/README.en.md) | コンパイル時 gate、実行時 gate、条件付き経路の手がかり |
| リポジトリを手早く回る | [SIMPLE/README.en.md](./SIMPLE/README.en.md) | 初見向けの短い読み方 |
| そのまま深掘りする | [DEEP/README.en.md](./DEEP/README.en.md) | ソース追跡向けの長い読み方 |

## 読み方の例

### ルート A：まず全体地図を作る

1. [ARCHITECTURE.en.md](./ARCHITECTURE.en.md)
2. [MODULES/README.en.md](./MODULES/README.en.md)
3. 任意のモジュールの `README.en.md`
4. 任意のモジュールの `SIMPLE/README.en.md`
5. 任意のモジュールの `DEEP/README.en.md`

### ルート B：共有主線から追う

1. [ARCHITECTURE.en.md](./ARCHITECTURE.en.md)
2. [01-agent-loop-and-teams/README.en.md](./MODULES/01-agent-loop-and-teams/README.en.md)
3. [02-planning-compaction-and-assistant/README.en.md](./MODULES/02-planning-compaction-and-assistant/README.en.md)
4. [03-persistent-memory-system/README.en.md](./MODULES/03-persistent-memory-system/README.en.md)
5. [05-tools-mcp-skills-and-plugins/README.en.md](./MODULES/05-tools-mcp-skills-and-plugins/README.en.md)
6. [06-permissions-sandbox-and-trust/README.en.md](./MODULES/06-permissions-sandbox-and-trust/README.en.md)

### ルート C：prompts、gate、遠隔経路から入る

1. [PROMPTS/README.en.md](./PROMPTS/README.en.md)
2. [FEATURE-FLAGS/README.en.md](./FEATURE-FLAGS/README.en.md)
3. [07-remote-session-bridge-and-sdk/README.en.md](./MODULES/07-remote-session-bridge-and-sdk/README.en.md)
4. [08-prompts-config-and-other-moats/README.en.md](./MODULES/08-prompts-config-and-other-moats/README.en.md)

## 主要ドキュメントとディレクトリ

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

最初の入口としては `README`、`ARCHITECTURE`、`MODULES`、`PROMPTS`、`FEATURE-FLAGS` から入ると流れをつかみやすくなります。`AI-AGENT/` は自動化向けの構造化補足レイヤーです。

## 読むときの境界

- これは非公式の研究リポジトリです
- ソース事実の範囲は `ChinaSiro/claude-code-sourcemap` とローカルの `_upstream/claude-code-sourcemap/` ミラーです
- `feature()`、GrowthBook、env gate は条件付き経路の存在を示すもので、公開 rollout をそのまま示すものではありません
- `Buddy`、`KAIROS`、`PROACTIVE`、`voice`、`bridge`、`remote isolation` などの名称は、ソース上の表現と周辺文脈の範囲で扱います

詳細な境界は [DISCLAIMER.md](./DISCLAIMER.md) を参照してください。

## 続けて読む

- [MODULES/README.en.md](./MODULES/README.en.md)
- [PROMPTS/README.en.md](./PROMPTS/README.en.md)
- [FEATURE-FLAGS/README.en.md](./FEATURE-FLAGS/README.en.md)
- [COMPARISONS/README.en.md](./COMPARISONS/README.en.md)
- [EXAMPLES/README.en.md](./EXAMPLES/README.en.md)
- [ASSETS/README.en.md](./ASSETS/README.en.md)
- [CONTRIBUTING.md](./CONTRIBUTING.md) / [CONTRIBUTING.en.md](./CONTRIBUTING.en.md)
- [SECURITY.md](./SECURITY.md) / [SECURITY.en.md](./SECURITY.en.md)
- [AI-AGENT](./AI-AGENT/)：自動化向けの構造化補足ノート
