# Claude・Codex に加える3つ目の生成AI候補（2026年10月時点）

> **参考資料**: Web 検索（標準・拡張）による調査の要約。調査日 2026-10-29〜10-30。
> 価格・上限の多くは第三者の比較記事による二次情報で、各社の公式料金ページでは確認できていない。契約前に公式ページを確認すること。
> 前提資料: [`2026-10-28-Codex主体-ClaudeCode補助の活用事例.md`](2026-10-28-Codex主体-ClaudeCode補助の活用事例.md)

作成 2026-10-30

---

## 選定条件

1. **定額制**であること（従量課金ではない）
2. 価格帯は **$100〜$125/月程度**（Claude でいう Standard $25 では不足、Premium $125 相当を想定）
3. 性能が Claude・Codex と**肩を並べる、または後を追える**可能性があること
4. できれば **VS Code 上で GUI（拡張機能）** で使え、**CLI でも操作できる**こと

---

## 結論

> **追記（2026-10-30）**: 以下の推奨は個人契約が前提。Google AI Pro / Ultra は法人では契約できず、法人の Gemini は Google Cloud 経由の席課金と従量課金になる。法人契約が前提の場合は [`2026-10-30-Gemini-Grokの法人利用プラン.md`](2026-10-30-Gemini-Grokの法人利用プラン.md) を参照。

- **2026年10月時点で、Claude・Codex と肩を並べる3つ目の選択肢はない。** 後を追える力があるのは、独自にフロンティアモデルを開発している Google（Gemini）と xAI（Grok）の2社。
- **推奨は Google AI Ultra 5x（$99.99/月）。** 予算に収まり、価格と上限の仕組みが最もはっきりしている。Google 公式の VS Code 拡張と CLI が揃っており、別系統のモデルによるクロスレビュー役としてすぐ役立つ。
- **Grok は次点。** 現時点のスコアは Gemini をわずかに上回るが、$100 前後のプランの存在が確認できず、上限も非公開。VS Code 拡張は有志によるもの。まずは SuperGrok（約 $30）で試す程度が安全。

---

## 1. 性能: FrontierCode 2.0（Cognition、2026-10-27 公開）

実際の PR をマージしてよいかを判定させる、難易度の高いベンチマーク。

| モデル | 開発元 | FrontierCode 2.0 | 旧版 1.1 |
|---|---|---|---|
| Claude Opus 5.5 | Anthropic | 45.5% | - |
| GPT-6 Astra（Codex） | OpenAI | 42.8% | - |
| Grok 4.7 | xAI | 28.6% | 47.6% |
| Gemini 4 Argon | Google | 26.3% | 47.5% |
| Kimi K3 | Moonshot | 17.7% | 44.2% |
| GLM 5.3 | Z.ai | 約17%（報道ベース） | - |

**読み取り**: 旧版 1.1 では Grok と Gemini も 47% 台で互角だったが、2.0 では上位2社に20ポイント近く引き離された。Kimi・GLM は安く使える選択肢としては良いが、このベンチマーク上では一段下。

**注意点**:
- 数値は Cognition が自社で測ったもので、課題は非公開のため第三者が再現できない。
- Gemini は Google 自身のツールではなく devin-cli 上で計測されているため、実際の使用感とずれる可能性がある。
- ベンチマーク1つだけでの比較である。

出典: [Cognition: FrontierCode 2.0](https://cognition.com/blog/frontier-code-2.0) / [BenchLM: FrontierCode 2.0 Leaderboard](https://benchlm.ai/benchmarks/frontiercode-2) / [AlphaSignal](https://alphasignal.ai/news/cognition-s-frontiercode-2-0-reveals-every-ai-coder-fails-half-of-real)

---

## 2. 定額プランの比較

| 候補 | 該当プラン | 価格（目安） | 評価 |
|---|---|---|---|
| **Gemini** | Google AI Ultra 5x | **$99.99/月** | Pro の5倍の枠（2026年5月に新設）。5時間ごとの枠と週の上限があり、超えた分は AI クレジットで追加できる。価格は複数の記事で一致。上位に Ultra 20x（$199.99）がある |
| **Grok** | SuperGrok Plus / Heavy | 約 $100 / 約 $300 | Plus は1つの記事にしか載っておらず未確認。上限は非公開で、チャットなど Grok の全製品と週の枠を共有する |
| Kimi | Max / Ultra | $99 / $199 | 価格は合うが、性能の条件を満たさない。中国企業のサービスのため、業務コードを送る場合はデータの取り扱いを確認する必要がある |
| GLM（Z.ai） | Pro / Max | $80 / $168 | 同上 |
| Cursor | Super | $100 | 中で使うモデルは結局 Claude と GPT が中心なので、3つ目の系統にはならない |
| GitHub Copilot | Pro+ | 約 $39（クレジット制） | 安いが、3つ目の系統という目的には合わない |

出典: [CloudZero: Antigravity pricing](https://www.cloudzero.com/blog/google-antigravity-pricing/) / [datastudios: Antigravity Ultra 5x/20x](https://www.datastudios.org/post/is-google-antigravity-free-to-use-pricing-limits-and-what-developers-should-expect) / [CodeAgentSwarm: Grok Build Pricing](https://www.codeagentswarm.com/en/guides/grok-build-pricing) / [CloudZero: Grok pricing](https://www.cloudzero.com/blog/grok-pricing/) / [AgentRiot: Grok Build Review](https://agentriot.com/news/ai-tools/grok-build-xai-coding-agent-300-dollar-pricing) / [Novita: Best AI Coding Plans](https://blogs.novita.ai/ai-coding-plans/) / [codingplan.org](https://codingplan.org/en)

---

## 3. VS Code 拡張（GUI）と CLI の対応状況

| | VS Code 拡張（GUI） | CLI | ほかのエディタ |
|---|---|---|---|
| **Gemini** | **公式あり**: Google 発行の「Antigravity」拡張（VS Code Marketplace）。無料プランから Ultra まで全プランで使える | **Antigravity CLI**（公式） | Antigravity 専用 IDE（VS Code 系）。JetBrains にも Antigravity 拡張があるという情報あり（未確認） |
| **Grok** | **公式なし**: 有志のオープンソース拡張「Grok Build for VS Code (Community)」（4.8万インストール超）。中では Grok Build CLI を ACP 経由で動かす | **Grok Build CLI**（公式。対話画面、`-p` のヘッドレス実行、ACP） | **Zed は公式に対応**（ACP Registry に登録済み）。JetBrains は有志のプラグインで、機能は不完全 |

※ ACP（Agent Client Protocol）: エディタとコーディングエージェントをつなぐ共通規格。

### Gemini の注意点（2026年に体制が大きく変わった）

- **単体の Gemini CLI と、個人向けの Gemini Code Assist 拡張は、2026年6月18日に提供終了**した。Pro や Ultra の契約者も対象。古い記事を見て Gemini CLI や Code Assist を入れても、個人プランでは動かない。今後使うのは Antigravity の拡張と Antigravity CLI。
- Gemini Code Assist の Standard / Enterprise は既存契約のみ継続（2026年10月9日以降は新規購入不可、2027年に終了）。
- Antigravity 拡張を入れるときは、発行元が Google になっているものを選ぶ。名前の似た非公式の拡張がある。
- Google AI のサブスクを使える VS Code 拡張は Google 公式のものだけ。サードパーティ製の拡張から個人サブスクを使う方法は、公式には用意されていない。

### Grok の注意点

- xAI（現 SpaceXAI）が公式に用意している使い方は、ターミナル、ヘッドレス実行、ACP の3つだけ。VS Code 拡張は xAI とは無関係の有志によるものなので、業務で入れる場合はソースコードを確認するなど、社内の審査が必要。
- Grok Build は Claude Code と互換性があり、既存のスキルや MCP の設定を引き継げるとされる。最大8つのサブエージェントを別々の Git worktree で並列に動かせる。
- 有志の拡張は Codex CLI と Claude Code CLI も ACP 経由で動かせるため、3つのエージェントを1つの画面にまとめる使い方もできる。

出典: [Antigravity 公式ドキュメント: VS Code 拡張](https://antigravity.google/docs/ide/extensions/vscode) / [Antigravity 公式ブログ: IDE 拡張](https://antigravity.google/blog/antigravity-ide-extensions) / [GitHub: Gemini CLI から Antigravity CLI への移行告知](https://github.com/google-gemini/gemini-cli/discussions/27274) / [Gemini Code Assist リリースノート](https://docs.cloud.google.com/gemini/docs/codeassist/release-notes) / [Lilach Bullock: Gemini Code Assist の変更点](https://www.lilachbullock.com/gemini-code-assist/) / [Google AI Developers Forum: サードパーティ拡張とサブスク](https://discuss.ai.google.dev/t/supported-gemini-subscription-access-for-a-third-party-vs-code-extension/189889/2) / [Zed: Grok Build ACP Agent](https://zed.dev/acp/agent/grok-build) / [Product Compass: Grok Build for VS Code](https://www.productcompass.pm/p/grok-build-vscode) / [GitHub: bhuertgen/grok-build-vscode](https://github.com/bhuertgen/grok-build-vscode) / [Lindy: Grok Build Explained](https://www.lindy.ai/blog/grok-build) / [codersera: Grok Build CLI Explained](https://codersera.com/blog/xai-grok-build-skills-connectors-guide-2026/)

---

## 4. 関連: Claude Code の画面から他社モデルを使う方法

[claude-code-with-codex](https://github.com/fcakyon/claude-code-with-codex)（MIT）は、手元で動くプロキシ（Rust 製 CLI `claude-codex`）。Claude Code の画面のまま、モデル名に応じて Claude・ChatGPT（Codex）・Kimi・Grok・Cursor のサブスクに振り分ける。会話の途中で `/model` で切り替えられ、前のモデルの思考内容も引き継がれる。

- 操作する画面（ハーネス）は Claude Code のままなので、Codex アプリや Antigravity のような各社のワークベンチの強みは得られない。
- Codex などのログイン情報を公式クライアント以外で使う仕組みのため、各社の利用規約上の扱いは確認が必要。
- `ANTHROPIC_API_KEY` / `ANTHROPIC_AUTH_TOKEN` を設定すると、Claude 側が 401 になる。

---

## 調査上の限界

- 価格と上限の大半は第三者の比較記事によるもので、記事どうしで食い違いがある（特に Grok の中間プランと Cursor の新旧プラン）。
- 性能比較は FrontierCode 2.0 の1つだけで、しかも開発元が自社で測った数値。
- Kimi・GLM の VS Code 拡張と CLI の対応状況は確認していない。
- 「3つ目として Gemini や Grok を足した開発者の実際の声」は、まだ収集していない（`/last30days` による追加調査の候補）。
