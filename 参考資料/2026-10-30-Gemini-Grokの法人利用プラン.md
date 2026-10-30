# Gemini・Grok を法人で使う場合の料金体系（2026年10月時点）

> **参考資料**: Web 検索（標準・拡張）と公式ページの確認による調査の要約。調査日 2026-10-30。
> 価格の一部は第三者による二次情報。契約前に各社の営業窓口と公式ページで確認すること（xAI の料金ページは取得時に 403 で確認できなかった）。
> 前提資料: [`2026-10-30-Claude-Codexに加える3つ目の生成AI候補.md`](2026-10-30-Claude-Codexに加える3つ目の生成AI候補.md) / [`2026-10-30-Gemini-Grokをメインで使う開発者の声.md`](2026-10-30-Gemini-Grokをメインで使う開発者の声.md)

作成 2026-10-30

---

## 要点

1. **Gemini には、法人が会社として契約できる「Ultra 5x のような1人あたり定額のプラン」がない。** 個人向けの Pro / Ultra は法人では使えず、Workspace 向けの Ultra アドオンも 2026年7月7日で提供終了した。
2. **法人の入口は Google Cloud 経由の2つ**: Gemini Enterprise の席課金（$30/席/月〜）と、従量課金のみのプラン（席料金 $0）。席課金でも Antigravity の枠は1人あたり月 $10〜$15 分しかなく、メインに近い使い方では費用の大半が従量課金になる。
3. **予算管理の仕組みは整っている。** プロジェクトごとの上限額、予算の通知、利用額を約束する割引があり、「上限付きの従量課金」として運用すれば実質的に予算を固定できる。
4. **Grok Business（約 $30/席/月）は定額だが、枠の量が非公開。** $100〜$125 程度の法人プランは見つからなかった。
5. **法人契約が前提なら、前回の「Google AI Ultra 5x を推奨」は取り下げる。**

---

## 1. Gemini（Antigravity）

### 個人向けプランは法人では使えない

- Workspace 向けの「AI Ultra Access」アドオンは **2026年7月7日で提供終了**。既存のライセンスは「AI Expanded Access」に自動で移行されたが、移行先には Antigravity・Gemini CLI・Gemini Code Assist のプラグインといった開発者ツールが含まれない（[フォーラム: AI Ultra Access 終了後の開発者の扱い](https://discuss.ai.google.dev/t/clarification-needed-path-forward-for-developers-after-ai-ultra-access-retirement/170853) / [フォーラム: Ultra 終了後の Antigravity](https://discuss.ai.google.dev/t/antigravity-access-after-ai-ultra-plan-ends/170980)）。いずれもユーザーによる告知の引用で、Google のヘルプページ本体は確認できていない。
- 提供終了の前から、Workspace アカウントでは Antigravity が途中で止まる（「Agent terminated due to an error」）という報告が多かった。個人アカウントでは問題なく動いたという（[フォーラム](https://discuss.ai.google.dev/t/bug-agent-terminated-error-makes-antigravity-completely-unusable-on-google-workspace-accounts-personal-accounts-work-fine/139683)）。
- 個人契約の Ultra に切り替えて業務に使う人もいる。しかしその場合は個人向けの利用規約が適用され、法人契約の Google Cloud 利用規約やデータ保護の条件は使えない。**会社として採用するなら避けるべき。**

### 法人の入口: Google Cloud 経由の2つ

[公式料金ページ](https://antigravity.google/pricing)の「Business plan via Google Cloud」:

| 方式 | 料金 | Antigravity の扱い |
|---|---|---|
| Gemini Enterprise Standard / Plus（席課金） | **$30/席/月〜**。Plus は年契約 $50（月契約 $60）という情報もあるが、1つの記事のみで未確認（[vdf.ai](https://vdf.ai/blog/gemini-enterprise-pricing-vs-private-ai/)） | 含まれるのは1人あたり月 **$10（Standard）/ $15（Plus）分のクレジットだけ**。超えた分は管理者が許可すれば従量課金 |
| 従量課金のみのプラン | 席料金 $0 | 使った分だけ請求。「一部の顧客から提供し、順次拡大」 |

**枠の仕組み**（[公式ドキュメント: Quotas and pay-as-you-go usage](https://docs.cloud.google.com/gemini/enterprise/docs/quotas-and-overages)）:

- 枠は同じプランの利用者全員で共有する。7日ごとの上限は「1人あたりの月額 ÷ 4 × 契約席数」。使わなかった分は繰り越さない。
- 枠を超えた分の従量課金は、管理者が設定で有効にしない限り使えない（無効なら枠で止まる）。請求書払いの Cloud Billing アカウントが必要。
- 超えた分の Gemini の利用料は Agent Platform（旧 Vertex AI）の料金で請求される。Antigravity で Claude モデルを使う場合は、枠に含まれず常に従量課金（例: Opus 5.5 は入力 $4.00 / 出力 $20.00 per 1M トークン）。

**提供状況**: Antigravity を Gemini Enterprise に含める形は「対象の顧客」への提供で、順次拡大中とされる（[Google Cloud ブログ「Flexible billing and cost controls for agents」2026-08-27](https://cloud.google.com/blog/products/ai-machine-learning/flexible-billing-and-cost-controls-for-agents-on-google-cloud)）。

### 予算管理の仕組み（同ブログ）

- **プロジェクトごとの上限額**: 月の上限額を設定でき、達するとそのプロジェクトのエージェントの API 呼び出しが止まる（ほかのインフラには影響しない）。ワンクリックで再開できる。
- **通知**: 予算の 50%・80%・100% でメール通知。異常な支出の増加を検知する機能もある。
- **利用額の約束による割引（Flexible Savings Plans）**: 月の利用額を約束すると、1年契約で 10%、3年契約で 20% 割引。枠を超えた分の従量課金にも適用される。

**読み取り**: 定額ではないが、チームやプロジェクト単位で上限額を「1人あたり $125/月前後 × 人数」に設定すれば、予算の上限は固定できる。ただし上限に達すると作業が止まる点は、定額プランの「枠切れ」と同じ。

---

## 2. Grok

| プラン | 料金 | 内容 |
|---|---|---|
| Grok Business | **約 $30/席/月（年契約で $25）**。オンラインで申し込める | 二次情報では、Grok Build を含み、標準で学習に使われず、SOC 2 Type II（第三者によるセキュリティ監査の認証）を取得、管理者向けの権限管理と一括請求がある |
| Grok Enterprise | 個別見積もり | SSO、専用インフラ、個別の利用上限、コンプライアンス対応など |

出典: [aipricing.guru: Grok Business](https://www.aipricing.guru/subscriptions/xai-grok-business/) / [TechRadar](https://www.techradar.com/pro/elon-musk-goes-all-in-on-smbs-with-new-grok-enterprise-and-business-offerings?rand=141) / [Lindy: Grok Pricing](https://www.lindy.ai/blog/grok-pricing) / [Meet Cody: Grok Enterprise](https://meetcody.ai/blog/grok-enterprise-pricing-features-security/)

- **枠**: 有料プランの枠は、チャット・画像・音声・Build など Grok の全製品で共有する「週ごとの枠」。長いコーディング作業はチャットよりはるかに多く消費する。超えた分は追加クレジットを買うか、自動チャージを有効にする（[xAI FAQ](https://docs.x.ai/grok/faq)）。Business の1席あたりの枠の量は公開されていない。
- **$100〜$125 程度の法人プランは見つからなかった。** 
- **Cursor との統合**: xAI の公式ドキュメントでは、Grok Bot が「Cursor のすべての有料プランに含まれる」とされ、チーム向けの管理（SSO・SCIM・管理画面）は Cursor のアカウントや管理画面で行う（[Grok Bot for teams and enterprises](https://docs.x.ai/grok-bot/teams-and-enterprises)）。前回の資料で未確認とした SpaceX による Cursor 買収説を裏付ける材料の1つになるが、Grok Build の法人での扱いはこのページには書かれていない。
- **データの扱い**: Grok Bot は、Cursor の Privacy Mode が有効なら顧客データを学習に使わない。設定を確認できない場合も学習しない側に倒す（同ページ）。Grok Business の保存期間や学習条件の公式な記載は見つからなかった。

---

## 3. 前回の推奨への影響

前回の資料では、個人契約を前提に **Google AI Ultra 5x（$99.99/月）を推奨**していた。**法人契約が前提なら、この推奨は取り下げる。** 法人の条件で並べ直すと次のとおり。

| 順位 | 構成 | 利点 | 欠点 |
|---|---|---|---|
| 1 | **Gemini Enterprise と従量課金の組み合わせ**。プロジェクトの上限額を Premium 相当（1人 $125/月前後）に設定する | 性能、公式の VS Code 拡張と CLI、Google Cloud の利用規約によるデータ保護 | 定額ではない。Antigravity の提供がまだ一部の顧客に限られる。Google の営業への確認が必要 |
| 2 | **Grok Business** | 定額で安い。申し込みが簡単 | 枠の量が非公開。性能・品質・セキュリティの懸念は前回と同じ。小規模に試すのに向く |

**確認すべきこと**（Google の営業窓口へ）:

- 自社が Antigravity を含む Gemini Enterprise の「対象の顧客」に入るか
- Plus の正式な価格と、$15 分のクレジットで実際にどれくらい作業できるか
- 従量課金のみのプランを使えるか

---

## 調査上の限界

- Workspace の AI Ultra Access 終了と、移行先に Antigravity が含まれないという情報は、フォーラムに引用された告知とユーザーの報告による。Google のヘルプページ本体は確認できていない。
- Gemini Enterprise Plus の価格、Grok Business の価格・Grok Build が含まれるか・SOC 2 の取得状況は二次情報のみ。
- xAI の料金ページ（x.ai/pricing）は取得時に 403 で、内容を確認できなかった。
- Claude（Team / Enterprise）・ChatGPT（Business / Enterprise）の法人プランとの比較はしていない。
