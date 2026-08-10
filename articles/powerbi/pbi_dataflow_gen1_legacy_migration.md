---
title: データフロー Gen1 の廃止について
date: 2026-06-30 00:00:00
tags:
  - Power BI
  - Microsoft Fabric
  - Dataflow
  - Dataflow Gen1
  - Dataflow Gen2
  - Data Factory
  - データフロー
  - 移行
  - Migration
  - Legacy
---

こんにちは、Power BI サポート チームの中川です。

2026 年 4 月に Fabric Community Blog にて、Power BI Dataflow Gen1 が Legacy 状態へ移行することがアナウンスされました。既存のデータフローは引き続き利用できますが、今後の新機能の提供や機能改善は Dataflow Gen2 のみに集中していくことが明示されています。

本ブログでは、アナウンスの要点やデータフロー Gen1 のサポートについてご案内いたします。 

<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
## 目次
---
* [Power BI / Fabric Dataflow Gen1 の今後について](#Power-BI-Fabric-Dataflow-Gen1-の今後について)
* [Dataflow Gen2 の主な強化ポイント](#Dataflow-Gen2-の主な強化ポイント)
* [Gen1 から Gen2 への移行方法](#Gen1-から-Gen2-への移行方法)
* [Dataflow Gen1 のサポートとお問い合わせについて](#データフロー-Gen1-のサポートとお問い合わせについて)
* [おわりに](#おわりに)


---
## Power BI / Fabric Dataflow Gen1 の今後について
---

Fabric Community Blog のアナウンス内容を整理いたしますと、現時点で確定している事項は以下のとおりです。

- 既存のデータフロー Gen1 は引き続き利用可能
- Gen1 への新機能追加は行われず、高インパクトな問題のみ修正対象
- 製品 UI 上で Gen1 アーティファクトには Legacy ラベルが表示される
- Premium 容量上の Gen1 廃止については、少なくとも 12 ヶ月前に通知される
- 廃止日は現時点（2026年6月）では未確定 

<div align="left">
<img src="dataflow_gen1_legacy.png">
</div>

</br>

### Gen1 は Legacy 状態へ、すべての新規イノベーションは Gen2 に投入

データフロー Gen1 は Legacy 状態に移行することが明示され、引き続き利用可能ですが、新機能は追加されません。 Gen1 の具体的な廃止日は現時点で確定しておらず、計画の進行に応じて詳細が共有される予定ですが、Premium 容量で Gen1 を実行しているお客様には、Dataflow Gen1 が廃止される少なくとも 12 ヶ月前に通知が行われます。 

なお、こうした方針（Legacy 状態、新機能追加なし、限定的なサポート、廃止日検討）は、Pro、PPU、Premium のすべてのライセンスにおける Gen1 に適用されると記載があります。 

</br>

### ライセンス・環境別のガイダンス

Fabric Community Blog では、ライセンス・環境ごとに以下のガイダンスが示されています。

| 区分 | 現状 | 推奨アクション | 補足 |
|---|---|---|---|
| Premium（Fabric 利用可能） | Gen1 は引き続きサポート対象 | Dataflow Gen2 への移行を検討 | パフォーマンス向上・AI 支援など Gen2 の最新機能をすぐに活用できます |
| Pro / Premium Per User (PPU) | Gen1 は引き続きサポート対象 | 現状の用途に最適であれば継続利用可 | Gen2 への移行パスが整備され次第、移行手順のガイダンスが共有される予定です |
| GCC（Premium） | Gen1 を利用中 | 移行マイルストーンの前に Gen2 サポートが提供される予定 | Gen1 の廃止タイムラインより前に GCC での Gen2 サポートが提供される予定です |

※ GCC（Government Community Cloud）：米国政府機関およびその関連組織向けに、各種コンプライアンス要件を満たすかたちで提供されるクラウド環境です。
</br>

>[!NOTE]
> 参考情報：[Dataflows: Thank you for eight years of Gen1—and why Gen2 is the future | Microsoft Fabric Blog](https://community.fabric.microsoft.com/t5/Power-BI-Updates-Blog/Dataflows-Thank-you-for-eight-years-of-Gen1-and-why-Gen2-is-the/ba-p/5173910)
> 参考情報：[Dataflow Gen1 から Dataflow Gen2 への移行 - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/data-factory/dataflow-gen2-migrate-from-dataflow-gen1)


---
## Dataflow Gen2 の主な強化ポイント
---

Fabric Community Blog では、Dataflow Gen2 の強化ポイントとして以下の 5 領域が紹介されています。本セクションでは、各領域の概要のみを一文で要約してご紹介いたします。

- **より柔軟な出力先**：SharePoint / OneDrive、Azure Data Lake Storage、Azure SQL Database / SQL MI、Fabric Lakehouse / Warehouse / SQL 分析エンドポイント、Snowflake などのクラウド データベースを[出力先として指定](https://learn.microsoft.com/ja-jp/fabric/data-factory/dataflow-gen2-data-destinations-and-managed-settings)できます。
- **パフォーマンスとスケールの向上**：Fabric ランタイムと最新の実行エンジン上で動作し、Fast Copy や並列実行などにより、Gen1 と比較して更新時間の短縮が見込めます。
- **AI による作成支援**：Copilot を活用した M クエリの自動生成、コード説明、フォールド可能性の推奨、データ品質の AI 分析などが組み込まれています。
- **詳細な診断・更新履歴**：更新ごとの詳細な時間情報、フォールド判定やコネクタ挙動のログなど、より詳細な診断情報が提供されます。
- **段階的（CU ベース）の価格モデルとコスト削減の可能性**：データフローの実行が Premium 容量の固定的な消費から切り離され、Fabric の容量ユニット（CU）ベースで使用分のみ課金されます。間欠的・季節的な更新パターンを持つワークロードでは、Premium 容量上で稼働する Gen1 と比較してコスト削減が見込まれる可能性があります。

</br>

各機能の差異については、弊チームのブログにて Gen1 / Gen2 の比較表をご紹介しておりますので、併せてご参考いただけますと幸いです。

>[!NOTE]
> 参考情報：[Power BI データフロー Gen2 と Gen1 の比較 | Japan CSS Support Power BI Blog](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_dataflow_gen1_gen2/)
> 参考情報：[Dataflow Gen2 データの格納先とマネージド設定 - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/data-factory/dataflow-gen2-data-destinations-and-managed-settings)

---
## Gen1 から Gen2 への移行方法
---

Fabric Community Blog では、Gen1 から Gen2 への移行について以下のアプローチが案内されています。本セクションでは、その概要をご紹介いたします。
</br>
### 移行を始める前に

移行作業に着手する前に、公式ドキュメントで紹介されている移行シナリオをご確認いただくことをお勧めいたします。公式ドキュメントでは、利用規模や利用形態ごとに想定される移行アプローチや推奨手順が紹介されておりますので、ご利用環境に近いシナリオを参考に、移行計画をご検討いただけますと幸いです。

>[!NOTE]
> 参考情報：[Dataflow Gen1 から Dataflow Gen2 への移行: 移行シナリオ - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/data-factory/dataflow-gen2-migrate-from-dataflow-gen1-scenarios)

</br>

### 個別移行：UI で「Dataflow Gen2 として保存」

Power BI / Fabric のワークスペース UI 上で、Gen1 を新しい Dataflow Gen2 として保存できます。手順は以下のとおりです。

1. ワークスペースで対象の Dataflow Gen1 の右側にある省略記号（…）を選択
2. コンテキスト メニューから [Dataflow Gen2 として保存] を選択
3. [名前を付けて保存] ダイアログで必要に応じて名前を変更し、[作成] を選択
4. 新しい Dataflow Gen2 (CI/CD) が開くので、内容を確認・修正
5. [保存] または [保存して実行] を選択

<div align="left">
<img src="dataflow_gen1_to_gen2.png">
</div>

</br>

>[!NOTE]
> 2026 年 4 月以降、CI/CD サポートなしの Dataflow Gen2（旧称：Dataflow Gen2 Classic）は新規作成できなくなりました。現在、新規の Dataflow Gen2 アイテムはすべて CI/CD 対応として作成されます。既存の Classic アイテムは引き続き動作しますが、新規作成はできません。
> 参考情報：[Dataflow Gen2 とは - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/data-factory/dataflows-gen2-overview)

なお、以下のシナリオでは Fabric が利用できないため、[Dataflow Gen2 として保存] 機能は無効化されます。

- Power BI Pro ワークスペース
- Power BI Premium Per User (PPU) ワークスペース
- テナント、容量、またはユーザー グループの管理者設定 「ユーザーは Fabric アイテムを作成できます」が無効になっている

>[!NOTE]
> 参考情報：[名前を付けて保存を使用して Dataflow Gen2 (CI/CD) に移行する - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/data-factory/migrate-to-dataflow-gen2-using-save-as)

</br>

### 大規模移行・自動化：REST API

複数のデータフローを一括で移行する場合や、CI/CD ワークフローに組み込んで自動化したい場合は、REST API(`Save Dataflow Gen One as Dataflow Gen Two`)を利用できます。

REST API では、`includeSchedule` により、元の Gen1 データフローの更新スケジュールを新しいアーティファクトへ無効状態でコピーするよう試行できます。ただし、スケジュールのコピーに失敗した場合でも、移行自体は成功として返され、エラー情報は応答の `errors` 配列に含まれる場合があります。

>[!NOTE]
> 参考情報：[Save Dataflow Gen One As Dataflow Gen Two - REST API (Power BI Power BI Dataflows) | Microsoft Learn](https://learn.microsoft.com/ja-jp/rest/api/power-bi/dataflows/save-dataflow-gen-one-as-dataflow-gen-two)

</br>

### Save as 移行時の既知の制限事項

[Dataflow Gen2 として保存] による移行には、現時点で以下の既知の制限事項があります。移行前にご確認のうえ、必要な再設定を計画いただくことをお勧めします。

- **スケジュール更新設定**:手動ではスケジュール更新はコピーされません。一方、Gen1 から Gen2 への REST API 移行では、`includeSchedule` により既存スケジュールを含めることができます。
- **増分更新設定はコピーされない**：移行後に増分更新ポリシーを再設定する必要があります。
- **Gen1 の一部機能は Dataflow Gen2 (CI/CD) には適用できないためコピーされない**：以下の機能が該当します。
  - CDM フォルダー
  - Bring Your Own Lake (BYOL)
  - コンピューティング エンジン
  - DirectQuery
  - AI Insights
  - 保証（Endorsements）

</br>

DirectQuery 接続については、Dataflow Gen2 ではデータ変換先機能を使用し、出力テーブルに直接接続する方式が推奨されています。

>[!NOTE]
> 参考情報：[名前を付けて保存を使用して Dataflow Gen2 (CI/CD) に移行する - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/data-factory/migrate-to-dataflow-gen2-using-save-as#known-limitations)


---
## データフロー Gen1 のサポートとお問い合わせについて
---

### サポート方針

データフロー Gen1 は Legacy 状態へ移行したものの、引き続きサポート対象となります。データフロー Gen1 に関する問題が発生した際には、これまでと同様に Microsoft サポートへお問い合わせいただけます。

ただし、Fabric Community Blog において、今後の データフロー Gen1 に対するサポートは「既存アーキテクチャ内で安全に変更を提供できる範囲の、高インパクトな問題の限定的なセット」に留まることが明示されています。そのため、以下のようなご依頼については、ご希望に沿えず対応が難しい場合がございます。

- インパクトの小さい製品不具合の修正
- データフロー Gen1 への新機能追加・機能改善のご要望

なお、既に解消しており再現しない一過性の事象につきましては、データフロー Gen1 / Gen2 （およびセマンティックモデル） を問わず調査を承りますが、事象の性質上、根本原因の特定が難しい場合がございます。
</br>

>[!NOTE]
> データフロー Gen1 で発生している事象が、データフロー Gen2 への移行により解消される可能性があります。Fabric 環境が利用可能であれば、 Dataflow Gen2 への移行をお試しいただくことを推奨します。

</br>



---
## おわりに
---

本ブログでは、2026 年 4 月にアナウンスされた Power BI データフロー Gen1 の Legacy 化とサポートについてご紹介いたしました。

データフロー Gen1 は引き続きサポート対象ですが、Legacy 状態となり、新機能投資は Dataflow Gen2 に集中していくことが案内されています。また、廃止に向かう方向性は Pro / PPU / Premium の データフロー Gen1 すべてに適用されます。一方で、Premium 容量で Gen1 を実行しているお客様には、少なくとも 12 ヶ月前に廃止通知が行われることが明示されています。

現時点で即時に全件移行が必要と案内されている状況ではありませんが、今後の新機能投資が Dataflow Gen2 に集中していくこと、また Premium 顧客向けには Gen2 が推奨パスとして案内されていることを踏まえますと、**新規開発は Dataflow Gen2 を選択**し、**既存 Gen1 についても移行計画の着手**を進めておくことをお勧めいたします。

Pro / PPU 向けの Gen2 パスや GCC 環境での Gen2 サポート、具体的な廃止スケジュールや通知条件などは、今後の公式アップデートで順次明らかになっていく見込みです。本ブログでも、新たなガイダンスが公開され次第、アップデートを予定しております。

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。


---
**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)

