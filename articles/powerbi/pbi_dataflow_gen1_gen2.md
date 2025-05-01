---
title: Power BI データフロー Gen2 と Gen1 の比較
date: 2025-04-30 16:00:00 
tags:
  - Power BI
  - Power BI サービス
  - Power BI Service
  - データフロー
  - データフロー Gen2
  - Dataflow
  - Dataset
  - Dataflow Gen2
---


こんにちは、Power BI サポート チームのチャンです。  
Power BI でデータの加工・データ準備を行う際によく使用されるデータフローに、現在は新たな選択肢として、新しい世代のデータフロー Gen2 をご利用いただけますが、実際本来のデータフロー (Gen1) とはどのような違いがあって、どのようなメリットやデメリットがあるか疑問点を持つ方も多くいらっしゃると思います。
本ブログにて、データフロー Gen1 と Gen2 の特徴と機能差異についてご紹介いたします。


<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
## 目次
---
1. [データフロー Gen1 とは？](#データフロー-Gen1-とは？)
2. [データフロー Gen2 とは？](#データフロー-Gen2-とは？)
3. [データフロー Gen1 と Gen2 の比較](#データフロー-Gen1-と-Gen2-の比較)
4. [データフロー Gen2 のデータ変換先を設定するときによくある問題](#データフロー-Gen2-のデータ変換先を設定するときによくある問題)


---
## データフロー Gen1 とは？
---
Power BI データフロー Gen1 は、以下の画像で示す通り、様々なデータ ソースからデータを取得して加工するフローのことで、ETL（Extract/Transform/Load）ツールに該当します。

<div align="center">
<img src="dataflow.png">
</div>

実際は、Common Data Model というサービスを使用しており、すべてクラウド上 (Azure Data Lake Storage Gen2 上) で動作するものでございます。
バックエンドでは Azure のリソースを使用していますが、別途 Azure のサブスクリプションを購入する必要がなく、データフロー Gen1 は、Power BI の Pro ライセンスのみでご利用いただけます。

UI 上の操作は、実は Power BI Desktop 内に付属している Power Query Editor とほとんど同様です。

<div align="center">
<img src="dataflow_powerquery_ui.png">
</div>

データフロー Gen1 は、端的に言えば、Power Query Editor のオンライン版としてご認識いただけます。
作成されたデータフロー Gen1 をレポートで利用するには、Power BI Desktop からデータフローに接続して、セマンティックモデルを構成する必要がございます。

> [!NOTE]
> // 参考情報 (1)：[Common Data Model](https://learn.microsoft.com/ja-JP/common-data-model/)
> // 参考情報 (2)：[Power BI and Dataflows (Power BI とデータフロー)](https://go.microsoft.com/fwlink/?linkid=2034388&clcid=0x409)

---
## データフロー Gen2 とは？
---

データフロー Gen2 は Fabric 容量または Fabric 機能を有効化した Premium 容量を利用する必要があり、 Pro ワークスペースでは作成することができません。また、Fabric 容量または Premium 容量が割り当てられたワークスペースでは、 Free ライセンスを持つユーザーでデータフロー Gen2 を作成いただけます。

データフロー Gen2 は、 Gen1 と同様に多数のデータ ソースへ接続して、 Power Query Editor の UI 操作でデータ加工・準備を行なうことが可能です。
データフロー Gen1 で作成した M クエリをそのまま Gen2 でも利用できます。一方で、データフロー Gen2 で接続可能なデータ ソースは Gen1 より多く、例えば Fabric レイクハウス、Fabric ウェアハウス コネクタはデータフロー Gen 2 でのみ利用可能です。

Gen1 との違いにつきましては、データフロー Gen2 は Fabric Data Factory の製品群に分類されます。アーキテクチャの面において、Gen2 の内部では、ステージング コンピューティングとステージング ストレージにレイクハウスを使用してデータ処理を行なっているため、より大量のデータを効率的に取り込むことができます。

<div align="center">
<img src="dataflows-gen2-diagram.png">
</div>

さらに、[高速コピー](https://learn.microsoft.com/ja-jp/fabric/data-factory/dataflows-gen2-fast-copy) という機能があり、該当機能がサポートされている特定のコネクタや変換内容に合致する場合、より高いパフォーマンスを実現できます。

また、データフロー Gen2 で変換処理されたデータの出力先として、 Fabric レイクハウス、Fabric ウェアハウス、Azure SQL Database などを選択して設定することが可能です。データの出力先として　Fabric レイクハウスか Fabric ウェアハウスと設定することで、セマンティックモデルからはそれらに対して [DirectLake モード](https://learn.microsoft.com/ja-jp/fabric/fundamentals/direct-lake-overview)で接続できます。

Fabric データパイプラインとの統合によって、パイプラインからデータフローのデータ更新をトリガーすることも可能となっております。

> [!NOTE]
> //参考情報 (1)：[Microsoft Fabric の Data Factory での Dataflow Gen2 の価格](https://learn.microsoft.com/ja-jp/fabric/data-factory/pricing-dataflows-gen2)
> //参考情報 (2)：[Dataflow Gen2 データの格納先とマネージド設定](https://learn.microsoft.com/ja-jp/fabric/data-factory/dataflow-gen2-data-destinations-and-managed-settings)
> //参考情報 (3)：[データフロー アクティビティを使用して Dataflow Gen2 を実行する](https://learn.microsoft.com/ja-jp/fabric/data-factory/dataflow-activity)
> //参考情報 (4)：[パイプラインでデータフローを使用する](https://learn.microsoft.com/ja-jp/fabric/data-factory/tutorial-dataflows-gen2-pipeline-activity)

---
## データフロー Gen1 と Gen2 の比較
---

以下にてデータフロー Gen1 と Gen2 の主な機能を比較した内容を表にまとめました。

|    | データフロー Gen1 | データフロー Gen2  | 
| ---- | ----| ---- | 
| ユーザーライセンス | Pro | Free 以上 | 
| ワークスペースのライセンス | Pro 以上  | Fabric 容量（試用版含む）または Premium 容量 | 
| Power Query データ ソースのサポート | 〇  | 〇   | 
| 自動保存 | ×  | 〇   | 
| スケジュール更新 | [〇](https://learn.microsoft.com/ja-jp/power-bi/transform-model/dataflows/dataflows-understand-optimize-refresh)  | [〇](https://learn.microsoft.com/ja-jp/fabric/data-factory/dataflow-gen2-refresh) | 
| 増分更新 | [〇](https://learn.microsoft.com/ja-jp/power-query/dataflows/incremental-refresh)  | [〇](https://learn.microsoft.com/ja-jp/fabric/data-factory/dataflow-gen2-incremental-refresh)   | 
| 更新タイムアウト | [Pro: 2 時間/テーブル、3 時間/データフロー <br> Premium: 24 時間/データフロー](https://learn.microsoft.com/ja-jp/power-bi/transform-model/dataflows/dataflows-features-limitations#general-limitations) | [24 時間/データフロー](https://learn.microsoft.com/ja-jp/fabric/data-factory/dataflow-gen2-refresh#refresh-limitations) |
| データフロー コネクタの DirectQuery  | [〇](https://learn.microsoft.com/ja-jp/power-bi/transform-model/dataflows/dataflows-directquery)  | ×  | 
| オンプレミス データゲートウェイの利用  | 〇  | 〇  | 
| VNet データゲートウェイの利用   | ×  | [〇](https://learn.microsoft.com/ja-jp/data-integration/vnet/use-data-gateways-dfgen2-fabric)  | 
| Cognitive Services AI 関数の利用（言語の検出、キー フレーズ抽出、センチメントのスコア付け、タグ イメージ） | [〇](https://learn.microsoft.com/ja-jp/power-bi/transform-model/dataflows/dataflows-machine-learning-integration)  | ×  | 
| Copilot for Data Factory の利用 | ×   | [〇](https://learn.microsoft.com/ja-jp/fabric/fundamentals/copilot-fabric-data-factory)  | 
| 高速コピー  | ×  | [〇](https://learn.microsoft.com/ja-jp/fabric/data-factory/dataflows-gen2-fast-copy)  | 
| データ変換先の設定 (レイクハウス・ウェイハウスなど） | ×  | [〇](https://learn.microsoft.com/ja-jp/fabric/data-factory/dataflow-gen2-data-destinations-and-managed-settings)  | 
| Fabric データパイプラインでの利用  | ×   | [〇](https://learn.microsoft.com/ja-jp/fabric/data-factory/dataflow-activity) | 
| 強化された更新履歴   | ×   | [〇](https://learn.microsoft.com/ja-jp/fabric/data-factory/dataflows-gen2-monitor)  | 
| 監視ハブの利用 | ×  | [〇](https://learn.microsoft.com/ja-jp/fabric/admin/monitoring-hub)  | 

> [!NOTE]
> //参考情報 (1)：[データフロー第1世代から第2世代への移行](https://learn.microsoft.com/ja-jp/fabric/data-factory/dataflows-gen2-overview)
>//参考情報 (2)：[Dataflow Gen1 から Dataflow Gen2 への移行](https://learn.microsoft.com/ja-jp/fabric/data-factory/dataflow-gen2-migrate-from-dataflow-gen1)

<p>

---
## データフロー Gen2 のデータ変換先を設定するときによくある問題
---

データフロー Gen2 でオンプレミスデータ ゲートウェイを使用する場合、該当データフロー Gen2 のデータ変換先をレイクハウスまたはウェアハウスに設定する際に、ポート 1433 に関するネットワーク問題が発生することがございます。

注意点として、<b>データ ソースのみ</b> オンプレミスデータ ゲートウェイを使用し、データの変換先の指定の際にオンプレミスデータ ゲートウェイを使用しない場合でもこちらの事例に該当します。

データ変換先の設定で、レイクハウスやウェアハウスへの接続の際に、以下のようなエラーが出力されます。

> Error: Microsoft SQL: A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible.

本エラーが発生する理由は、レイクハウスからデータを読み取る場合は、TDS プロトコル (TCP 1433 番ポート) を使用する必要があるためです。ステージングレイクハウスからデータの変換先にデータをコピーするためにデータを読み取り、 TCP 1433 番ポートが使用されます。

エラーを解消するには、ゲートウェイ サーバーのネットワーク環境のファイアウォール規則に以下の条件を追加します。

> プロトコル: TCP
> エンドポイント: *.datawarehouse.pbidedicated.windows.net, *.datawarehouse.fabric.microsoft.com, *.dfs.fabric.microsoft.com
> ポート: 1433

しかしながら、ゲートウェイサーバーの外部通信に、プロキシサーバーをご利用の場合は、プロキシサーバー側に上記の規則を許可いただいても通信することができません。
原因としては、オンプレミスデータゲートウェイ製品のプロキシ設定の仕様上、TCP 1433 番ポートの通信をプロキシサーバー経由でルーティングさせることができないからです。

ゲートウェイサーバーの外部通信に、プロキシサーバーをご利用の場合の回避策としては、以下のいずれかが考えられます。

- オンプレミスデータ ゲートウェイをインストールしている端末環境で、プロキシサーバー経由以外に外部への通信が許可されている通信ルートを別途用意する
<i>または</i>
- データフロー Gen2 を 以下の通り 2 つに分割する [※](https://learn.microsoft.com/ja-jp/fabric/data-factory/gateway-considerations-output-destinations#workaround-split-dataflow-in-a-separate-ingest-and-load-dataflow)
  (1) オンプレミスデータ ゲートウェイを使用して、データ ソースへの接続やデータ変換をするデータフロー
  (2) ゲートウェイ使用せず、上記のデータフローを参照しながら、データの変換先をレイクハウス・ウェアハウスとして設定するデータフロー


> [!NOTE]
> //参考情報：[Dataflow Gen2 のデータのコピー先に関するオンプレミス データ ゲートウェイの考慮事項](https://learn.microsoft.com/ja-jp/fabric/data-factory/gateway-considerations-output-destinations)

> **本ブログの関連記事**
> - [Power BI データフローとデータセット及びデータマートの紹介と比較](../pbi_dataflow_dataset)
> - [Power BI ライセンスの違い（Free・Pro・Premium Per User・Premium Per Capacity・Embedded）](../pbi_license/)

</br>

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)