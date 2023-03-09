---
title: Power BI データフローとデータセット及びデータマートの紹介と比較
date: 2022-08-31 00:00:00 
tags:
  - Power BI
  - Power BI サービス
  - Power BI Desktop
  - データフロー
  - データセット
  - Dataflow
  - Dataset
  - データマート
  - Datamart
---


こんにちは、Power BI サポート チームのチャンです。  
Power BIでデータを加工したり、データ準備を行う時、よくデータフローやデータセットなどの言葉を耳にしますが、実際それぞれどのような違いがあって、どの場面で使うか疑問点をお持ちの方も多くいらっしゃると思います。
本ブログにて、データフローとデータセットの詳細、及び執筆時点ではプレビュー機能のデータマートについてもご紹介いたします。

<span style="color: red; ">
Update: 2022/8/31</br>
データマート機能のご紹介部分に関して、より深く紹介するために内容を修正し、比較表にも追加しました。
詳しくは [データマートについて]と[データマート、データフロー、データセットの比較]セクションをご覧ください。
</span>
</p>

<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
## 目次
---
1. [データフローとは？](#データフローとは？)
2. [データセットとは？](#データセットとは？)
3. [データマートについて](#データマートについて)
4. [データマート、データフロー、データセットの比較](#[データマート、データフロー、データセットの比較)

---
## データフローとは？
---
Power BIデータフローは、以下の画像で示す通り、様々なデータソースからデータを取得して加工するフローのことで、ETL（Extract/Transform/Load）ツールに該当します。

<div align="center">
<img src="dataflow.png">
</div>

実際は、Common Data Modelというサービスを使用しており、すべてクラウド上（Azure Data Lake Storage Gen2上）で動作するものでございます。
バックエンドではAzureのリソースを使用していますが、別途Azureのサブスクリプションを購入する必要がなく、データフローは、Power BIのProライセンスのみでご利用いただけます。

UI上の操作は、実はPower BI Desktop内に付属しているPower Query Editorとほとんど同様です。

<div align="center">
<img src="dataflow_powerquery_ui.png">
</div>

データフローは、端的に言えば、Power Query Editorのオンライン版としてご認識いただけます。

Power Query Editorで行なうデータ加工をオンラインで実行することの（データフローを利用する）メリットについては、以下が挙げられます。

- データ加工のフローを他のユーザーと簡単に共有できること。
- クラウド上でデータ加工を実施することは、端末のスペックに依存しないこと（ただし、サーバーのスペックに依存する）。
- データソースへの接続はデータフローのみで、複数のユーザーがデータソースへのアクセスを最小限に抑えること
- 一部データフロー（Power Query Online）のみ利用可能な機能がある。例えば[ダイアグラムビュー](https://learn.microsoft.com/ja-jp/power-query/diagram-view)や[スキーマビュー](https://learn.microsoft.com/ja-jp/power-query/schema-view)など。

> [!NOTE]
> // 参考情報 (1)：[Common Data Model](https://learn.microsoft.com/ja-JP/common-data-model/)
> // 参考情報 (2)：[Power BI and Dataflows (Power BI とデータフロー)](https://go.microsoft.com/fwlink/?linkid=2034388&clcid=0x409)

---
## データセットとは？
---

データフローをはじめ、Power BI Desktopから様々なデータソース（例えばSQL Server、Excelなど）に接続して、データモデルを定義する必要があります。Power BIデータセットは、データモデルが定義されるもので、実際使用されている技術は、 Analysis Services 表形式モデルでございます。

<div align="center">
<img src="dataset.png">
</div>
 
Analysis Servicesはデータ分析用のデータエンジンの技術で、Power BIをはじめ、
Excel、Reporting Services、その他のデータ視覚化ツールなどでも使用されている技術です。

> [!NOTE]
> // 参考情報：[Power BI サービスのデータセット](https://learn.microsoft.com/ja-jp/power-bi/connect-data/service-datasets-understand#power-bi-desktop-developed-models)


---
## データマートについて
---

2022年5月24日にパブリックプレビュー機能としてリリースされた「データマート」についてもご紹介します。

<div align="center">
<img src="datamart2.png">
</div>

データマートとは、データフローとデータセットを一つに融合して、Power BI内でAzure SQL Databaseの環境を使用した機能でございます。
ユーザー側で様々なデータソースを集約してPower BIサービス上に「データマート」内でデータウェアハウスを作成し、他のユーザーと共有することができます。

データマートを使用するメリットは以下の点が挙げられます。
- Power BI Desktopからデータセットを作成する必要がなく、ETLのフローからデータのモデリングまですべてクラウド上で完結できます。
- インポートしたデータに対して、レポートを作成せずともクイックに分析を行う（クエリを作成する）ことができます。その分析方法は、グラフィックUI上でノーコードでの実施、または、SQLによるクエリの実行も可能となります。さらにSQLで実施した結果をExcelへエクスポートすることもできます。
- 外部のツール（Azure Data Studio やSQL Server Management Studio）から接続することが可能で、より高度な管理や統計を行える上、Windows以外のOS環境からの接続も簡単になります。
- 共有の操作はデータフローやデータセットより簡易的になり、組織内のユーザーやグループとセキュリティが有効な共有ができます。

現在は、Premium容量とPremium Per Userのみ使用できる機能でございます。
詳細につきましては、以下のブログ記事（英語）とドキュメントよりご確認ください。

> [!NOTE]
> // 参考情報 (1)：[データマートの概要](https://learn.microsoft.com/en-us/power-bi/transform-model/datamarts/datamarts-overview)
> // 参考情報 (2)：[Announcing public preview of datamart in Power BI](https://powerbi.microsoft.com/ja-jp/blog/announcing-public-preview-of-datamart-in-power-bi/)
> // 参考情報 (3)：[データマートの分析](https://learn.microsoft.com/ja-jp/power-bi/transform-model/datamarts/datamarts-analyze)

> [!IMPORTANT] 
> 本機能は開発段階 (プレビュー)でございますため、今後予告なしに機能が削除されたり、
> 動作変更が発生する可能性がありますことをあらかじめご了承くださいますようお願い申し上げます。

---
## データマート、データフロー、データセットの比較
---

|                          | データマート                                        | データフロー                                                                 | データセット                        | 
| ------------------------ | --------------------------------------------------- | ---------------------------------------------------------------------------- | ----------------------------------- | 
| 一言で言うと             | セルフデータウェアハウス                            | ETLツール                                                                    | データモデル                        | 
| 説明                     | ETLツールとデータモデリング機能を一つに集約したもの | データソースから抽出、変換、ロード                                           | DAXの使用とリレーションシップの設定 | 
| 利用者                   | すべてのビジネスユーザー、分析者                                              | データモデリングの実施者                                                     | レポート作成者                      | 
| 使用言語                 | 操作箇所によって[M言語](https://learn.microsoft.com/ja-jp/powerquery-m/)、[DAX]((https://learn.microsoft.com/ja-jp/dax/))、SQLも利用可能           |[PowerQuery M言語](https://learn.microsoft.com/ja-jp/powerquery-m/)                                                             | [DAX](https://learn.microsoft.com/ja-jp/dax/)                                 | 
| 編集操作場所             | Power BIサービス（クラウド）                        | Power BIサービス（クラウド）                                                 | Power BI Desktop（ローカル）        | 
| レポートからの接続       | 〇（データセットが自動的に作成される）              | ×（Power BI Desktopでデータセットを作成する必要がある）                      | 〇                                  | 
| 必要なライセンス | Premium Per User / Premium Per Capacity             | Pro / Premium Per User /      Premium Per Capacity / Embedded                                                 | Free / Pro / Premium Per User / Premium Per Capacity / Embedded     | 
| Direct Query             | ×                                                   | 〇（Premium容量が必要）※1                                                   | 〇                                  | 
| インポート               | 〇                                                  | 〇                                                                           | 〇                                  | 
| データ更新のタイムアウト | 24時間                                              | Pro：2時間/テーブル、3時間/データフロー<br>Premium：24時間/データフロー　※2 | Pro：2時間<br>Premium：5時間　※3   | 
| 増分更新                 | 〇                                                  | 〇（Premium機能、Pro利用不可）※4                                            | 〇 ※5                              | 
|                          | 


※1：[データフローで DirectQuery を使用する](https://learn.microsoft.com/ja-jp/power-bi/transform-model/dataflows/dataflows-directquery)
※2：[データフローに関する考慮事項と制限事項](https://learn.microsoft.com/ja-jp/power-bi/transform-model/dataflows/dataflows-features-limitations)
※3：[Power BI でのデータの更新](https://learn.microsoft.com/ja-jp/power-bi/connect-data/refresh-data#data-refresh)
※4：[データフローでの増分更新の使用](https://learn.microsoft.com/ja-jp/power-query/dataflows/incremental-refresh)
※5：[データセットの増分更新とリアルタイム データ](https://learn.microsoft.com/ja-jp/power-bi/connect-data/incremental-refresh-overview)

<p>

> **本ブログの関連記事**
> - [Power BI サービスのデータセット更新手順について](../pbi_refresh_settings/)
> - [「インポート」と「Direct Query」データセットの違い](../storage_mode/)
> - [「テーブルの列 ‘***’ が見つかりませんでした。」Power BI更新エラーについて](../pbi_refresh_error/)
> - [Power BI ライセンスの違い（Free・Pro・Premium Per User・Premium Per Capacity・Embedded）](../pbi_license/)

</br>

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)
