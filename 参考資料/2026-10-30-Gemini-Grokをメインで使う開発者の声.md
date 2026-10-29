# Gemini・Grok をメインで使う開発者の声（2026年10月時点）

> **参考資料**: `/last30days` スキルによる調査結果の要約。対象期間 2026-09-29〜2026-10-29。
> ソース: Reddit 25 / X 14 / Hacker News 14 / YouTube 3 / GitHub 1 / Web 18（＋Web 補完検索 3回）。
> 元データ: [`logs/gemini-antigravity-or-grok-build-as-main-coding-agent-raw-gemini-grok-main.md`](../logs/gemini-antigravity-or-grok-build-as-main-coding-agent-raw-gemini-grok-main.md)
> 前提資料: [`2026-10-30-Claude-Codexに加える3つ目の生成AI候補.md`](2026-10-30-Claude-Codexに加える3つ目の生成AI候補.md)

作成 2026-10-30

---

## 要点

1. **Gemini をメインにする動機は、Argon・Carbon によるモデル性能の追い上げ**。ただしコーディングエージェントとしては、Claude Code にあと一歩届いていない。
2. **Antigravity を日常的に使う上での最大のリスクは、性能ではなく枠（クォータ）の不安定さ**と、プランごとに使えるモデルが変わること。
3. **最新モデルを Antigravity で使うには Ultra が前提**。Pro では足りない。
4. **Grok Build をメインにしていると語る一次投稿はほぼ見つからなかった**。複数のエージェントを並べる中の1つとして使われている。
5. **ベンチマークの順位より「自分のタスクと、今使っているハーネスで試す」**ことを勧める声が出ている。

---

## 1. Gemini: 熱量はここ2週間のモデル発表に集中

| 出来事 | 反応 |
|---|---|
| 10月13日、Antigravity に Gemini 4 Argon が登場（[公式ブログ](https://antigravity.google/blog/gemini-4-argon-in-google-antigravity)） | r/google_antigravity の [「Antigravity + Gemini 4 Argon - crazy insane!」](https://www.reddit.com/r/google_antigravity/comments/1xicgky/antigravity_gemini_4_argon_crazy_insane/) が 280pt・90コメント |
| 10月28日、Gemini 4 Carbon を発表 | r/GeminiAI の [「Gemini 4 Carbon: just... WOW」](https://www.reddit.com/r/GeminiAI/comments/1xhw48g/gemini_4_carbon_just_wow/) が 801pt・325コメントで最大のスレッド |
| YouTube での比較 | [Matt Wolfe「Google Just Caught Up (Gemini-4 Argon)」](https://www.youtube.com/watch?v=eBszYxzE2dk)（27.5万再生）、[Jack Roberts「Gemini 4 Argon vs Opus 5.5 Building the Same App」](https://www.youtube.com/watch?v=xq6S6g6BWnc)（8.1万再生） |

過熱ぶりはコメント欄でもネタにされている。[u/rangorn](https://reddit.com/r/GeminiAI/comments/1xibkef/comment/19rthuwykvl5s/)「Speaks Spanish and will insult your mother?」（63票）、[u/apatheticcreator](https://reddit.com/r/GeminiAI/comments/1xibkef/comment/19rtelr88im76/)「Always nice when someone types out the whole spec sheet before the pitch deck's even warm.」（46票）。

### Carbon はモデル単体では首位、コーディングエージェントとしては2位

| 指標 | Gemini 4 Carbon | 比較 |
|---|---|---|
| Artificial Analysis Intelligence Index v5（総合） | **1位（59）** | - |
| Artificial Analysis Coding Agent Index | 2位（59、Antigravity CLI 上） | Claude Code + Opus 5.5 が 62 |
| FrontierSWE 2 | 61.2% | GPT-6 Astra が 65.5% |

- [@Magnosud](https://x.com/Magnosud/status/2115854031935394043):「As a coding agent, it's still #2」。乗り換える前に、リーダーボードで選ぶのか、自分のタスクで試すのか、今使っているハーネスで選ぶのかを考えるよう促している。
- **Carbon は現在、一部のユーザー（サイバー防御の用途）にしか提供されていない。** Antigravity や Ultra プランで使えるかは未確認。

出典: [Artificial Analysis（X）](https://x.com/ArtificialAnlys/status/2115494553780367384) / [VentureBeat](https://venturebeat.com/technology/google-unveils-gemini-4-carbon-retaking-the-worlds-no-1-spot-on-updated-harder-benchmarks-but-access-is-limited) / [The Decoder](https://the-decoder.com/google-deepmind-releases-gemini-4-carbon-just-two-weeks-after-argon-with-gains-across-the-board/) / [OfficeChai](https://officechai.com/ai/gemini-4-carbon-benchmarks/)

---

## 2. Antigravity をメインにした人の不満: 性能より枠

- **枠の不安定さ**: 3月の料金改定以降、「何日も作業できない」「7日待ってもリセットされない」という声が続いている。Ultra 契約者からも「本番の作業には使えない」という投稿がある（[Google AI Developers Forum](https://discuss.ai.google.dev/t/google-antigravity-secret-quota-cuts-break-trust-make-it-unusable-for-production/136147) / [The Register](https://www.theregister.com/2026/03/12/users_protest_as_google_antigravity/) / [Techzine](https://www.techzine.eu/news/devops/139547/developers-complain-about-google-antigravity-pricing-structure)）。
- **プランによる違い**: Argon を Antigravity で使えるのは Ultra 契約者のみ（Pro も対象とする情報もあり）。r/google_antigravity では [「このプランでも Argon と Claude 5.5 を使えるか」](https://www.reddit.com/r/google_antigravity/comments/1xhump1/if_i_subscribe_in_this_offer_can_i_still_get/)（55コメント）のような質問が目立つ（[Google の告知](https://x.com/Google/status/2110041305925484716)）。
- **他社モデルの除外**: [@maune1_](https://x.com/maune1_/status/2115782450928562413)「Google pulled Claude/GPT from my discounted AI Pro in Antigravity」。割引価格の Pro では Claude と GPT が外されたという報告。
- **複数アカウントでの回避**: [「複数の Gemini Pro アカウントを Antigravity で使えるか」](https://www.reddit.com/r/google_antigravity/comments/1xim070/can_i_use_multiple_gemini_pro_accounts_in/)（14コメント）という質問も出ている。

---

## 3. Grok Build: メインにしている声はほぼない

- [xai-org/grok-build](https://github.com/xai-org/grok-build) のスター数は 2.76万（Apache-2.0、Rust）。注目度は高い。
- メインで使っている具体例は [@vernons](https://x.com/vernons/status/2115753916025750006) くらいで、それも「Antigravity の Gemini 3.5 Flash、OpenCode の DeepSeek、ローカルの Qwen」と並ぶ候補の1つという扱い。
- **評価されている点**: 8つのサブエージェントを別々の Git worktree で並列実行できること、実行前に変更内容を確認できる Plan Mode。ただし並列化が効くのは大規模な移行やテストの追加などで、小さな作業では調整の手間が増えるだけという指摘もある。
- **不満**: 「黙ってコードを書き換える」「料金がわかりにくい」「出力のエラー」。SWE-Bench Verified は 70.8%（Claude Code は 87.6%）とされる。
- **周辺の話題**: r/grok は [「What happened to grok?」](https://www.reddit.com/r/grok/comments/1xifpbs/what_happened_to_grok/) のような品質への不満が中心。HN では [「Grok Bot が CEO の銀行情報を公開 Slack に流出」](https://www.techdirt.com/2026/10/19/whoops-grok-bot-spills-tech-ceos-bank-data-in-public-slack/)（36pt）。

出典: [DEV: Grok Build Hype vs Reality](https://dev.to/dishant0406/grok-build-hype-vs-reality-a-look-at-real-user-reactions-48hg) / [ChatForest](https://chatforest.com/reviews/xai-grok-build-coding-agent-cli-review-2026/) / [layer3labs: Is Grok Build Worth It?](https://www.layer3labs.io/guides/is-grok-build-worth-it) / [Contra Collective: Grok Build vs Claude Code](https://contracollective.com/blog/grok-build-vs-claude-code-xai-coding-agent-2026)

---

## 4. その他の動き

- **Grok を各社サブスクの「元請け」にする構成**（中華圏）: [@LiuweijiaVip](https://x.com/LiuweijiaVip/status/2115829954600697922) が、Grok Bot のクラウド端末に Codex CLI・Claude Code・Antigravity CLI をつなぎ、各社の余った枠で24時間作業させる構成を紹介。本人も、ログイン状態をすべてクラウドに置くためトークン漏えいのリスクがあると認めている。
- **SpaceX による Cursor 買収説**: [@xulijian1994](https://x.com/xulijian1994/status/2115827318799446125) が「SpaceX が Cursor を600億ドル評価で買収し、Cursor の能力が Grok に統合されつつある」と投稿。**一次情報では未確認。**
- **Google の製品整理**: [@solomonneas](https://x.com/solomonneas/status/2115887905076130293) によると、Jules は12月31日に終了（11月11日以降は読み取り専用）。6月の Gemini CLI 終了に続き、Google のコーディング製品は Antigravity に一本化されつつある。
- **VS Code で複数エージェントを1画面に**: [phuryn/grok-build-vscode](https://github.com/phuryn/grok-build-vscode) は Grok Build に加えて Codex・Claude Code・（実験的に）Antigravity にも対応。

---

## 前回の推奨（Google AI Ultra 5x）への影響

| | 内容 |
|---|---|
| 追い風 | Argon と Carbon で性能差が縮まった。最新モデルは Ultra 限定のため、Ultra 5x を選ぶ理由はむしろ強まった |
| リスク | 枠への不満が根強く、Ultra でも不安定だという声がある。年契約にせず、月契約で実際の作業量を試すのが安全 |
| Grok | メインで使っている人の声がほぼなく、品質やセキュリティの話題も目立つ。次点のまま |

---

## 調査上の限界

- Reddit は投稿タイトルとエンゲージメント数が中心で、本文やコメントまで取れたスレッドは少ない。
- YouTube の文字起こしは3本中1本しか取得できなかった。
- X の投稿は14件と少なく、中国語圏の投稿が上位に入っている。
- Gemini 4 Carbon は発表直後で、実際に Antigravity で使った開発者の声はまだない。
- SpaceX による Cursor 買収と Grok への統合は、X の投稿のみが情報源で、一次情報では確認できていない。
