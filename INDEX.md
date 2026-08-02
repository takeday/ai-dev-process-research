# 先進的な生成AI開発プロセス — 調査インデックス

収集日: 2026-07-31 〜 2026-08-01 / エンジン: last30days v3.8.2 / 全9ラン・合計 **997件**

目的: 昼 Claude Code・夜 Codex のような、開発現場をドラスティックに変えるアイデアを広く収集する。**採用実績が少ないもの（新語彙・少数事例）を意図的に拾う**設計。

---

## 実行設定（全ラン共通）

```
--plan <5サブクエリのJSON>  --deep  --emit=compact  --store
--save-dir ~/Documents/Last30Days/ai-devprocess  --save-suffix <ラン名>
```

プランは全ラン `intent: "how_to"` / `freshness_mode: "evergreen_ok"` / `cluster_mode: "workflow"`。

**設計上の3つの選択**（それぞれエンジンのコードに基づく）:

1. **`--plan` を必ず渡した** — 渡さないとサブクエリが1本しか生成されない（前回実行の実測: 1本・36件）。1サブクエリ＝独立した取得ストリームなので、5本にすると母数が桁で変わる
2. **`intent: "how_to"` を明示した** — サブクエリ上限は intent 依存で、`concept` 判定だと2本で頭打ちになる。`how_to` なら5本通り、かつ鮮度ペナルティが外れて数週間前の少数事例が沈まなくなる
3. **1周目の topic を `AI` で始めた** — エンジンは topic の先頭トークンを含まない候補を25点減点する（素点レンジ 30〜70）。`Claude Code ...` で始めると Codex や汎用エージェントの投稿が全滅するため、あえて汎用語で無効化した。**2周目は逆に固有名を先頭に置いて減点を絞り込みとして使った**

代償: 1周目は無関係な語（CSS background / Spec CPU / car spec 等）が混入している。広く拾うためのトレードオフ。

---

## ラン一覧

### 1周目（英語・軸ごと / `--days` 既定30日）

| # | ファイル | topic | 件数 | 内訳 |
|---|---|---|---|---|
| A | `ai-coding-agents-running-unattended-workflows-raw-overnight.md` | AI coding agents running unattended workflows | 115 | HN 61 / X 46 / Reddit 6 / GitHub 1 / YT 1 |
| B | `ai-multi-agent-parallel-coding-workflows-in-practice-raw-multiagent.md` | AI multi agent parallel coding workflows in practice | 106 | X 52 / HN 48 / Reddit 4 / YT 2 |
| C | `ai-spec-driven-development-workflows-in-practice-raw-specdriven.md` | AI spec driven development workflows in practice | 51 | HN 23 / X 15 / Reddit 12 / YT 1 |
| D | `ai-coding-assistant-productivity-measurement-in-production-raw-metrics.md` | AI coding assistant productivity measurement in production | 99 | GitHub 40 / HN 34 / Reddit 14 / YT 7 / X 4 |

### 日本語補完（`LAST30DAYS_YT_SUB_LANGS=ja,en` / `--subreddits` なし）

| # | ファイル | topic | 件数 | 内訳 |
|---|---|---|---|---|
| JP | `ai-raw-jp.md` | AI 開発プロセス 事例 ワークフロー | 43 | GitHub 25 / X 11 / HN 4 / YT 3 |

Reddit は 0件（想定どおり。日本語話題は英語圏コミュニティにほぼ存在しない）。GitHub 25件の多くは個人リポジトリの日本語 Issue で、これが国内の生の実践ログになっている。

### 2周目 — 新語彙の二次探索（`--days=60`）

| # | ファイル | topic | 件数 | 内訳 |
|---|---|---|---|---|
| T1 | `loop-engineering-coding-agent-practice-raw-term-loop-engineering.md` | Loop Engineering coding agent practice | 168 | YT 50 / GitHub 49 / HN 44 / X 22 / Reddit 3 |
| T2 | `agent-harness-meta-harness-claude-code-codex-raw-term-harness.md` | Agent harness meta harness Claude Code Codex | 124 | YT 40 / HN 33 / X 27 / GitHub 21 / Reddit 3 |
| T3 | `orchestrator-tax-parallel-coding-agents-limits-raw-term-limits.md` | Orchestrator tax parallel coding agents limits | 103 | X 44 / HN 43 / GitHub 9 / YT 4 / Reddit 3 |
| T4 | `graph-engineering-agent-workflows-raw-term-graph.md` | Graph engineering agent workflows | 188 | GitHub 71 / X 42 / YT 39 / HN 30 / Reddit 6 |

---

## 新語彙リスト（1周目での出現頻度が低い順 = 二次探索の選定根拠）

「1周目クラスタ」は A〜D + JP の全クラスタタイトル中の出現数。**少ないほど採用実績が薄く、狙った層**。

| 語 | 1周目クラスタ | 2周目の結果 | 判定 |
|---|---|---|---|
| **The Orchestrator's Tax** | 1 (B) | T3 で定義に到達 | 定義は取れたが単独の広がりは小さい。周辺の反証群として価値 |
| **Loop Engineering** | 3 (A・B・C 各1) | **T1: 168件・YT 50件** | 当たり。1周目では各軸1件だったが、実際は急拡大中の概念 |
| **Graph Engineering** | 3 (B 2・C 1) | **T4: 188件（最大）** | 当たり。Loop の次段として論争が進行中 |
| **Harness / meta-harness** | 8+ (A 4・B 2・C 3) | T2: 124件 | 1周目時点で既に多め＝相対的に主流化が進んでいた語 |
| Coding Model Stack | 1 (B) | 未実施 | 未追跡 |
| Spec drift (SDD) | 1 (C) | 未実施 | 未追跡 |
| Worktree Pattern | 2 (B) | T3 に反証込みで包含 | — |

**この調査での最大の発見は語彙の階層そのもの**（T1 の X 投稿・T4 で複数確認、Web記事層で定義が確定）:

```
prompt engineering → context engineering → harness engineering → loop engineering → graph engineering
```

Web層（MarkTechPost / Prefect / explainx.ai）による定義:

> **プロンプトは1回のモデル応答を制御する。ループは1体のエージェントの行動サイクルを制御する。グラフは多数のエージェントの「組織」を制御する。これらは競合する技術ではなく、積み重なった3つの制御単位である。**

**導入順序を決める但し書き**: 「グラフはループを内包する。グラフの各ノードはループである。**弱いループの上に build されたグラフは、より多くの場所で同時に壊れるだけ**」。マルチエージェント構成より先に、1体が自力で完了に到達するループを固めること。

**Loop Engineering の出自**: 2026年6月に命名。Boris Cherny（Claude Code 作者）と Peter Steinberger（OpenClaw 作者）の言及で拡散。**語の歴史は1〜2ヶ月しかない** — 1周目で各軸1件ずつしか出なかったのは新しさが理由で、実質が薄いわけではなかった。arXiv に "Agentic Harness Engineering" 論文も既にある。

---

## ファイル別の注目項目（本文への入口）

### A — 夜間 / 24h自動運転
- **Ruflo** / **Agent Mesh** / **Agent-Manager**（tmux TUI で Claude Code・Codex・OpenCode を並走）— 昼夜切替構想の既存実装
- 「遊休 Claude Max サブスクを追加課金ゼロで 24/7 AI ops に転用」（X）
- **Curated Claude Code** — intake gate 付きハーネス（チケット受入の発想と同型）
- **Tuneloop** — エージェントのセッショントランスクリプト解析
- 反対意見: **"My Agent Isn't Autonomous. That's the Point"**
- ノイズ注意: "background" 一致で CSS / background check 等が約10クラスタ混入

### B — マルチエージェント並列
- **MindFlock / Shikigami / Fractal / Orca / Daemon / Abralo / Termic** — worktree ごとの並列実行系
- **MemU** — Codex・Claude Code・Hermes で共有する個人メモリ
- 反証: **「git worktree は隔離境界ではない」**、**「エージェントを増やしても速くならない（キューが伸びるだけ）」**、**The Orchestrator's Tax**

### C — 仕様駆動・要件自動化（最も薄い: 51件）
- **"If You Can Write Acceptance Criteria, You Can Write an AI Routing Policy"** — 受入条件が書ける人材の再定義
- **AgentCall** — コーディングエージェントを会議の参加者として同席させる
- **Memsprout** — AIコンテキストのチーム共有
- **GitHub Spec Kit / Forall / Speck / Great Spectations** — SDD ツール群
- 失敗モード: **"How to handle drifting Spec in SDD"**（仕様ドリフト）
- ノイズ注意: "spec" が Spec CPU / car spec / spec decode と衝突
- **Web記事層（末尾に追記済み）**: GitHub / Thoughtworks / Microsoft の一次資料、**Planning Agent パターン**（シニアが訊く明確化質問を返して受入条件に変換）、SDDは2026年時点で主要8ツールが実装済み。**「議事録→仕様」だけはWeb層でも事例が薄く、空白地帯として記録**

### D — 効果測定・ROI
- **Wattage** — トークン支出プロファイラ＋**コスト回帰ゲート**（CIで単価劣化を止める）
- **Epistemic Engine** — AI生成コードの検証と破綻予測
- **"The Real Cost of Unmeasured Code"**（YT）
- Reddit: **"Maintaining team velocity despite coding agents"**、**"2yrs at current company. new project is 99% ai generated. i don't know how to handle"**
- HN: **"Ask HN: How are you handling production risks from AI generated code?"**
- ノイズ注意: GitHub 40件の大半は無関係なPRタイトル
- **Web記事層（末尾に追記済み）が本命**。DORA 2025の数値（PRレビュー時間 **+441%**、レビューなしマージ **+31%**、組織デリバリーは横ばい）、Claude Code公式アナリティクス＋OTelで取れる指標一覧、マージPRあたりコスト **$0.28〜$89.32**、PRスループット向上 **+7.76%（中央値）**

### JP — 日本語
- **「AIエージェントを増やしたのに、成果が-70%落ちた理由」**（X）— 国内の定量的失敗事例
- **「【完全版】24時間自走する『自律型AIエージェント』の設計図」**（X）
- **「レビュー結果を学習し、観点・Skill・自動検査へ昇格する仕組み」**（GitHub Issue）
- **「今日、半日かけてAI3体分の『社内規定』を改定していました」** — エージェント単位のガバナンス文書
- **herdr**（agent-aware multiplexer）、**commandmate verify / wait --require-work**（完了検証CLI）、**サブエージェントのパラメータを front-matter で固定**
- 「2026年 企業のAIエージェント導入はどこまで進んだか｜Anthropic調査500社の実態」（YT）

### T1 — Loop Engineering
- 中核メカニズム: **「本物のテストが出荷前に失敗を露出させるとき、反復作業は手動プロンプトなしで回る」**
- "Stop Prompting Claude. Start Loop Engineering." / "5 Levels of Loop Engineering" / "Andrew Ng's three nested loops"
- 反対: **"FORGET Loop Engineering. Agentic Engineering is about THIS"**
- 失敗モード: **kanin-loop** — エージェント↔タスクの所有権が未管理だと git identity 共有で無言の衝突が起きる

### T2 — Agent harness / meta-harness
- **Omnigent** — Claude Code / Codex / Cursor / カスタムを1箇所で束ねる OSS メタハーネス。解説動画10本以上
- **"Running an Agent Meta-Harness As A Software Factory"** — 組織運用としての語り
- **cmux** / **Agent-talk** / **Supapool**（エージェント1体ごとに Supabase を約400msで払い出す）
- 「メモリとセキュリティを Claude Code・Cursor・Codex に与えるハーネスに 235,000 スター」
- リスク: **CVE-2026-59726**（エージェントプラットフォームの重大な脆弱性）

### T3 — 限界・反証（判断材料として最重要）
- **orchestrator tax の定義**（X）: 「最大のボトルネックは君自身の記憶と注意力」
- Reddit: **Orca のエージェント艦隊が「効く場合／トークンを5倍焼くだけの場合」と先に置くべきガードレール2つ**
- GitHub CRITICAL: **サブエージェント生成バグによる無限再帰・無限トークン消費・蓄積作業の消失**
- Reddit: **「セッション上限に達したとき、文脈と決定事項をどう別エージェントへ引き継ぐか」** — 昼夜切替で必ず当たる問題
- X: 「1年前に agentic coding は使えないと判断した会社が、その判定を今も維持している」
- 過激枠: **Oak / Grit**（エージェント向けに Git を作り直す）、**Buzz**（チャット＋エージェント＋Gitホスティング統合）

### T4 — Graph Engineering
- 定義: **「複数の専門エージェントが互いに仕事を受け渡す設計」**、"Why AI Agents Are Ditching While Loops"
- **「Graph engineering はエージェントを信頼できるものにするが、統治可能にはしない」**（X）— 統制の観点
- "Is Loop Engineering Already Obsolete?" / "Graph Engineering, Without the Hype" / "You used Graph Engineering incorrectly"
- 日本語記事も出現（GitHub: 「Graph Engineeringについての記事を追加」）

---

## 未消化 / 次にやるなら

- **Coding Model Stack** と **Spec drift (SDD)** は新語彙として抽出したが二次探索していない
- 軸C（仕様駆動）が51件と薄い。`--days=60` と "spec" 以外の言い換え（requirements / intent / contract）で再実行する余地
- 軸D の X が4件と弱い。計測系の語彙は X の投稿タイトルと噛み合っていない
- ~~`grounding`（Web検索）は全ランで0件~~ → **全9ラン分をホスト側WebSearchで後追い取得済み**（各ファイル末尾の「Web記事層」節）。エンジンの `grounding` は0件のままだが、そのレイヤは埋まっている
- Web層の取得は本来 Claude Code のホスト検索が担う（`CONFIGURATION.md:295` の優先順位で第1層）。ヘッドレス/cron実行でも埋めたい場合のみ `BRAVE_API_KEY` を設定する
- Reddit は全ランで一貫して薄い（3〜14件）。取得窓が `month` 固定で `--days=60` が効かない仕様も影響
- ScrapeCreators 未設定のため TikTok / Instagram / Reddit コメントは未取得
