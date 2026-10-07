# Claude Code と Codex の併用 — 事例と工夫（2026年9月時点）

> **参考資料**: `/last30days` スキルによる調査結果の要約。対象期間 2026-08-28〜2026-09-27。
> ソース: Reddit 15 / X 20 / Hacker News 17 / YouTube 3 / GitHub 2 / Web 19（＋日本語記事の補完検索）。
> 元データ: [`logs/claude-code-codex-combined-workflow-raw-codex-combo.md`](../logs/claude-code-codex-combined-workflow-raw-codex-combo.md)

作成 2026-09-28

---

## 要点

1. **最も再現性が高いのは「異なるモデル系統によるクロスレビュー」**。Claude Code で実装し、Codex にレビューさせる。
2. **「作った側は採点しない」**。計画を相互レビューしてから、実装とレビューの役割を入れ替える。
3. **ツールではなく工程で割り振る**。考える／作る／レビューする、を別々のエージェントに担当させる。
4. **併用の最大の課題は文脈の共有**。ルール・Skills・セッションで得た知見を両ツールに行き渡らせる仕組みが必要。
5. **2つのエージェントを動かすなら隔離もまとめて**。サンドボックスVMと、信頼できないリポジトリへの注意。

---

## 1. クロスレビュー（Claude Code が書き、Codex がレビュー）

| 手段 | 内容 |
|---|---|
| [openai/codex-plugin-cc](https://github.com/openai/codex-plugin-cc) | OpenAI 公式。Claude Code の中から Codex を呼び出すプラグイン。`/codex:review`（通常レビュー）と `/codex:adversarial-review`（「この変更は壊れている」前提で、出荷すべきでない理由を探す読み取り専用レビュー）がある。タスクの委譲やセッションの引き継ぎも可能 |
| [claudex-loop](https://github.com/chaseai-yt/claudex-loop) | Claude Code／Codex 両対応のスキル。①調査 ②問い詰め ③Codex による敵対的レビュー ④役割を入れ替えて実装・検査、の4段階。原則は「作った側は採点しない（Whoever built it never grades it）」 |
| MCP 経由の相互呼び出し | [mcp-agents](https://github.com/thomaswitt/mcp-agents) などで Claude Code／Codex を MCP ツールとして公開し、どちらからでもセカンドオピニオンを依頼できる |

**なぜ効くか**: 同じモデルは自分の判断の盲点を共有しやすい。「経緯を知らない他人の目で『本当に動くか』を問う」役として別系統のモデルを置く。中国語圏の実践者（@NFTCPS）も「AI の出力は候補にすぎない。重要なものは新しいセッションで見直す」と書いている。

---

## 2. 工程による役割分担

| パターン | 出典 |
|---|---|
| 「考える／作る／深掘る」を ChatGPT・Claude・Codex で分担。ただし「良いテイストは AI からは得られない」 | [@jodavid444dave](https://x.com/jodavid444dave/status/2104127956926796087) |
| Copilot が書き、Claude Code が考え、Codex がレビュー | [Zenn: 適材適所の実践ガイド](https://zenn.dev/motowo/articles/codex-claude-code-copilot-2026) |
| GitLab CI に両方のレビューを組み込み、ツール別にコストを計測（例: Codex $10.8、Claude Code $77.4） | [Qiita: GitLab CI + Claude Code + Codex](https://qiita.com/ktat/items/ab527d5e8e8e48d2b6db) |
| Claude・Codex・Gemini の「セカンドオピニオン運用フレーム」 | [Qiita: nogataka](https://qiita.com/nogataka/items/b2b4a84ba611ccaf8447) |

**得意分野に関する現場の評価（2026年9月末の声）**

- computer use（画面を操作させる機能）は Codex が優位という声 — [@blueemi99](https://x.com/blueemi99/status/2104243356138119225)
- リモートでの作業フローは Claude Code が優位という声 — [@twader_](https://x.com/twader_/status/2104199456547872795)
- 以前は「Codex が詰まったところだけ Claude」だったが、Claude Code（Opus 5.5）＋MCP に一本化した例 — [@RealDanRyland](https://x.com/RealDanRyland/status/2104132116258627611)

**コスト面の動機**: $20 のプランを2つ契約する方が $100 プラン1つより安く、利用上限を分散できる（[morphllm](https://www.morphllm.com/comparisons/codex-vs-claude-code)）。上限の厳しさに応じて主力を乗り換える人も多い。

---

## 3. 文脈と記憶の共有

併用で最も手間がかかるのは「片方で得た知見がもう片方に伝わらない」こと。

| 課題 | 対策の例 |
|---|---|
| ルールファイルの二重管理（Claude Code は `CLAUDE.md`、Codex は `AGENTS.md` を読む） | ルール・Skills・hooks を1か所で管理し、両方から参照させる — [Qiita: 共存セットアップ](https://qiita.com/kirozero/items/aec53be56a5427475969) |
| セッションで見つけた修正が次のツールに引き継がれない | Agent Beacon（Claude Code／Cursor／Codex のセッション履歴から教訓を抽出） — [@prayag_dalal](https://x.com/prayag_dalal/status/2104122609357226343) |
| 過去のやり取りを探せない | [Contextify](https://contextify.sh/windows/)（Claude Code／Codex の履歴をライブで索引化） |

---

## 4. 両方を束ねるオーケストレーター（2026年9月に出てきたもの）

| ツール | 概要 |
|---|---|
| [oto-dock](https://github.com/OtoDock/oto-dock) | セルフホストの「会社OS」。Claude Code／Codex のエージェントを部署ごとに配置（HN 50pt） |
| [Castforge](https://castforge.ai/) | Claude Code・Codex・Gemini を1つの開発チームとして動かす |
| [Ax](https://useax.dev/) | Claude・Codex・OpenCode をローカルで相互に会話させる |
| [AgentPulse](https://github.com/jerriclynsjohn/tmux-agent-pulse) | 両エージェントの状態を tmux に表示 |
| Omnigent | オープンソースのメタハーネス。設定・ポリシー・レビュー・ビルドを統合（[Leon van Zyl の解説動画](https://www.youtube.com/watch?v=gYtQ1LKSgXY)、13.8K 再生） |

**設計上の示唆**: r/vibecoding で「ガバナンス用プラグインとオーケストレーターの違いは？」と聞かれた作者は「同じものの別レイヤー」と答えている。**ガバナンス層**（ゲート、敵対的レビュー、リスク分類）と**実行層**（どのエージェントに何をさせるか）を分けて考える。なお、CLI をシェル経由で呼ぶ構成は呼び出しのたびにトークンを消費する、という報告もある（r/LocalLLM）。

---

## 5. 隔離とセキュリティ

- [Coop](https://github.com/trailofbits/coop)（Trail of Bits）: Claude Code と Codex を動かすための隔離 VM 環境（HN 71pt）
- [GitSpawn](https://www.manifold.security/blog/ai-coding-agents-git-hijack): 信頼できないリポジトリが Claude Code・Codex・Cursor 等でコードを実行できてしまう脆弱性の報告

---

## 本アーカイブとの関係

- [`01-業界動向-共有.md`](../01-業界動向-共有.md) の「メタハーネス（Omnigent）」: 7〜8月の調査では「両方を1か所で切り替える器」が製品化されたことを扱った。本資料（9月）は、その上での運用、つまりどちらに何をさせ、どうレビューさせるかを扱っている。
- [`logs/agent-harness-meta-harness-claude-code-codex-raw-term-harness.md`](../logs/agent-harness-meta-harness-claude-code-codex-raw-term-harness.md)（T2）: 同じテーマで60日分を集めた先行ラン。§4 のオーケストレーター群と比べると、この間の変化を追える。

---

## 調査上の限界

- 期間が30日と短く、X の投稿は 9/27 付近に偏っている。
- Reddit で反応が大きかったのは「どちらが優れているか」という比較の議論で、併用手順の具体例は Web 記事と GitHub のツールが中心。
- YouTube の文字起こしは取得できなかったため、動画については説明欄の内容のみを参照した。
