# Codex 主体・Claude Code 補助の活用事例と利用者の見解（2026年10月時点）

> **参考資料**: `/last30days` スキルによる調査結果の要約。対象期間 2026-09-27〜2026-10-27。
> ソース: Reddit 11 / X 53 / Hacker News 11 / YouTube 2 / GitHub 1 / Web 18（＋Web 補完検索 3回）。
> 元データ: [`logs/codex-as-primary-coding-agent-with-claude-code-as-secondary-raw-codex-primary.md`](../logs/codex-as-primary-coding-agent-with-claude-code-as-secondary-raw-codex-primary.md)

作成 2026-10-28

---

## 要点

1. **Codex を主力にする理由は、モデルの賢さより使用量上限とコストの予測しやすさ**。コードの質では Claude を上とする声が Codex ユーザーの間でも多い。
2. **Codex の強みは「ワークベンチ」としての完成度**。アプリ・クラウド・GitHub 連携まで含めた作業環境と、体感の速さが評価されている。
3. **最も具体的な分担は「Codex が実装し、Claude Code が独立レビュー」**。ただし逆向きの事例も多く、本質は「書いた側と別のモデルにレビューさせる」こと。
4. **併用の手間がそのまま課題になっている**。スキル同期、worktree の散らかり、レビュー役のエージェントがコードを書き換えてしまう問題など。
5. **好みは振れ幅が大きい**。7〜9月中旬は Codex 派が優勢だったが、10月上旬には Claude Code 側に揺り戻している。「Codex が主、Claude Code が補助」で固定した一次投稿は、この30日間では少数派。

---

## 1. Codex を主力にする理由: 上限・コスト・可用性

| 見解 | 出典 |
|---|---|
| 「コードの質は Claude Code が上だが、上限に達するのが早すぎて毎日の主力にしにくい」。Codex は「推論の天井は低めでも、いつでも使えてコストが読める」 | [vexp Blog: Codex vs Claude Code: What Reddit Developers Think](https://vexp.dev/blog/codex-vs-claude-code-reddit) / [DEV: What 500+ Reddit Developers Really Think](https://dev.to/sangrokjung/claude-code-vs-codex-2026-what-500-reddit-developers-really-think-31pb) |
| 上限まで使い切る文化。「Codex（20x）の残り3%を Codex に捧げた」スレッド（471pt）に「I think Codex just made a place to bury him.」 | [r/codex](https://www.reddit.com/r/codex/comments/1xgy2gh/i_gave_my_last_3_of_my_codex_20x_usage_towell/) |
| ヘビーユーザーはどちらも月 $100〜$200 帯で、コストはほぼ互角。上限の差が効くのは $20 プラン | Web 補完検索（比較記事のまとめ） |

**読み取り**: 「Codex のほうが賢いから」ではなく、「止まらずに使い続けられるから」主力にしている、という構図。

---

## 2. Codex 派の忠誠心と、Claude 優位を認める声

r/codex では、Codex 派の強い主張と、ベンチマークでは Claude が上だと認める声が同時に出ている。

| スレッド | 反応 |
|---|---|
| [「Opus 5.5 sucks, do NOT migrate to claude!!」](https://www.reddit.com/r/codex/comments/1x07or9/opus_55_sucks_do_not_migrate_to_claude/) | 897pt・212コメント。Claude への移行を止める立場 |
| [「This straight up feels like an advertisement for claude」](https://www.reddit.com/r/codex/comments/1xg4wkp/this_straight_up_feels_like_an_advertisement_for/) | 1,011pt。トップコメントは [u/TheOnlyBliebervik](https://reddit.com/r/codex/comments/1xg4wkp/comment/19rp005dsgmzl/)「Hard to believe that Astra max scores below sonnet 5.5」（216票）。[u/Fabulous-Mushroom124](https://reddit.com/r/codex/comments/1xg4wkp/comment/19rp0ogdy8yuc/) は「OAI seems to be focusing on cost」（111票） |
| [Cognition FrontierCode 2.0 の結果](https://www.reddit.com/r/codex/comments/1xh1uiu/cognition_has_released_frontiercode_20_a_tougher/) | 186pt。Claude Opus 5.5 が 45.5%、GPT-6 Astra が 42.8% |

**読み取り**: Codex ユーザー自身も性能面での Claude 優位を認めたうえで、コスト重視で Codex に留まっている。

---

## 3. Codex の強み: ワークベンチとしての完成度と速度

- 乗り換えの理由はモデル IQ ではない。「Claude Code still sounds like a coding tool first. Codex now sounds like a whole workbench.」 - [DEV: Why Developers Are Switching From Claude Code to Codex](https://dev.to/dishant0406/why-developers-are-switching-from-claude-code-to-codex-3ba0)
- Codex は推論が長い一方で、体感の出力は速い。GitHub 連携と価格ではまだ Codex が勝つ（Claude Code も UX で差を縮めた） - [Builder.io: Codex vs Claude Code](https://www.builder.io/blog/codex-vs-claude-code)
- 新モデルについて「It's VERY VERY fast compared to Sol 6.1」 - [r/codex](https://www.reddit.com/r/codex/comments/1xgtpco/even_codex_doesnt_know_what_to_say_about_this/)
- 運用の定石: AGENTS.md で指示範囲を絞り、変更したファイル・実行したコマンド・残ったリスクの要約を必ず出させる。同じ修正が2回出たら AGENTS.md を更新する - [Pasquale Pillitteri: Claude Code から Codex への移行ガイド](https://pasqualepillitteri.it/en/news/1862/from-claude-code-to-codex-developer-migration-guide-2026)

---

## 4. 分担パターン: Codex が実装し、Claude Code がレビュー

| 手段 | 内容 |
|---|---|
| [kevkzumi/skills issue #2](https://github.com/kevkzumi/skills/issues/2) | Codex がクリーンなリポジトリで仕様や issue を実装し、最終化の前に Claude Code の独立レビューを受けるクロスレビューのフローをスキル化 |
| [Unstoppable Code の Pipelines](https://x.com/unstoppableweb/status/2114789163858112888) | 「have Codex implement a change, Claude review it, and a script run your tests」を保存・再実行できる。ステップごとにエージェントとモデルを選べる |
| [DEV: Claude Code + Codex のルーチンをパイプライン化](https://dev.to/azaran/i-turned-my-claude-code-codex-routine-into-a-repeatable-pipeline-open-source-local-first-392k) | 「Claude で計画、承認、実装、テスト、Claude と Codex でレビュー、P0/P1 を修正、ドラフト PR」をグラフとして実行 |
| [DEV: Codex に Claude Code のコミットをレビューさせる](https://dev.to/iliyaoblakov/how-to-make-codex-review-claude-codes-commits-done-means-house-rules-and-round-rules-2ili) | 逆向き（Claude が書き Codex がレビュー）。「完了の定義」「ハウスルール」「ラウンドルール」を決める |
| [Damian Galarza: My Agentic Coding Workflow](https://www.damiangalarza.com/posts/2026-10-21-agentic-coding-workflow/) | Claude Code・Codex・Pi を組み合わせた個人ワークフロー（HN） |

**読み取り**: 役割を固定することより、「書いた側と別系統のモデルにレビューさせる」ことが重視されている。9月の調査（[Claude Code と Codex の併用](2026-09-28-ClaudeCode-Codex併用の事例と工夫.md)）では「Claude Code が書き Codex がレビュー」が主流だったが、10月は逆向き（Codex 実装・Claude レビュー）の事例も製品化され始めた。

---

## 5. 併用の課題と、それを埋めるツール

r/codex の [「Best way to get Codex and Claude Code working together?」](https://www.reddit.com/r/codex/comments/1x805d9/best_way_to_get_codex_and_claude_code_working/) に挙がった不満:

- アプリ間の切り替えが面倒
- workflow.md やスキルを常に更新し続けるのが大変
- worktree の管理が散らかる
- 「review agents modify the code instead of just reviewing」（レビュー役のエージェントが、レビューだけでなくコードを書き換えてしまう）
- 複数タスクを同時に見渡しにくい

これを埋めるツール:

| ツール | 内容 |
|---|---|
| [MuscleMemory](https://github.com/TheWariend/MuscleMemory) | Codex が学んだスキルを Claude Code で再利用する |
| [claude-code-with-codex](https://github.com/fcakyon/claude-code-with-codex) | Claude と ChatGPT（Codex）のサブスクを同時に使い、会話の途中で切り替える |
| [Pi-cowboy](https://github.com/electric-dragon-80000v/pi-cowboy) | Codex・Claude Code・OpenCode をサブエージェントとして使う（Show HN） |
| [Littleguys](https://littleguys.hervalicio.us) | Claude Code・Codex・OpenClaw のエージェントをメニューバーで管理（Show HN） |
| [@alimwtf の取り組み](https://x.com/alimwtf/status/2114646694935646318) | 「59日で250 PR をマージ」。Claude Code と Codex が互いに警告し合う仕組み |

チームでの課題として、「PM は ChatGPT、エンジニアは Claude Code・Cursor・Codex とバラバラだと、協業時に Slack とコピペに戻ってしまう」という声もある（[r/ChatGPTCoding](https://www.reddit.com/r/ChatGPTCoding/comments/1xg3k5z/claude_code_has_agent_teams_but_how_do_teams/)）。

---

## 6. 好みの振れ幅と逆方向の移行

- 2026年7月〜9月中旬は、どちらかを選んだ開発者の間で Codex 派が最大 4:1 で優勢。10月上旬には Claude Code 側に揺り戻した。両方を使う層は少数だが安定して存在する - [The Neuron: The vibe shift on the timeline is turning against Claude Code](https://www.theneuron.ai/explainer-articles/the-vibe-shift-on-the-timeline-is-turning-against-claude-code)
- 逆方向の例: 「switched from $200 Codex plan to $200 Claude」。Codex のほうが「polished」だが、安定性は Claude 側が上 - [@MartinMachava1](https://x.com/MartinMachava1/status/2114382194776965439)
- Cursor の料金変更をきっかけに「来月から Claude Code か Codex に移る」 - [@utekaravinash](https://x.com/utekaravinash/status/2114994121580662985)

---

## 本アーカイブとの関係

- [`参考資料/2026-09-28-ClaudeCode-Codex併用の事例と工夫.md`](2026-09-28-ClaudeCode-Codex併用の事例と工夫.md): 9月の併用調査。Claude Code を主・Codex をレビュー役とする事例が中心だった。本資料はその逆、Codex を主力とする側の見解に焦点を当てている。
- [`01-業界動向-共有.md`](../01-業界動向-共有.md) のメタハーネス（Omnigent）: 両方を1か所で切り替える器。§5 のツール群はその延長線上にある。

---

## 調査上の限界

- Reddit 検索の一部がレート制限（403/429）を受け、取得できたスレッドは11件に留まる。
- X は Safari の Cookie を読めず（macOS のフルディスクアクセス未許可）、認証付き検索が十分に機能しなかった可能性がある。
- YouTube の文字起こしは一部しか取得できなかった。
- 「Codex が主、Claude Code が補助」を明示的に語る一次投稿は少なく、§1〜3 の多くは比較記事や Reddit 意見のまとめ記事を経由した二次情報。数値（4:1 など）は一次データで確認できていない。
