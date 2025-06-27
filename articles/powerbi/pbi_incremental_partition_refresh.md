---
title: Power BI の増分更新における初回更新のタイムアウトを回避する方法
date: 2025-06-27 00:00:00 
tags:
  - Power BI
  - xmla endpoint
  - partition
  - incremental refresh
  - 増分更新
  - Power BI サービス
  - Power BI Service
---
こんにちは、Power BI サポート チームの呂です。

Power BI では、大規模データをより効率的に更新するために 、「増分更新」機能が用意されています。この機能を活用することで、すべてのデータを毎回再読み込みする必要がなくなり、直近で変更があったデータのみに対象を絞って更新することが可能になります。
一方で、Power BI サービスにレポートを発行し、セマンティックモデルの初回更新を実行する際には、設定された保持期間全体のデータが一括で取得されるため、処理時間が長くなり、タイムアウトが発生することがあります。本記事では、こうした初回更新時のエラーを回避する手順を紹介します。

<!-- more -->
> [!IMPORTANT]  
> 本記事編集時点と実際の機能に相違がある場合がございます。予めご了承ください。
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。


## 初回更新が失敗する主な原因とその回避アプローチ
Power BI の増分更新では、「アーカイブ期間（データ保持期間）」と「増分更新期間」を指定できますが、初回更新時には保持期間全体のデータが一括で処理されるため、タイムアウトが発生しやすくなります。
この問題を回避するには、Premium 容量で利用できる XMLA エンドポイントを使い、Tabular Editor や SSMS からパーティションを段階的に手動で更新する方法が有効です。初回処理を小分けにして順に完了させることで、保持期間全体の一括処理を避けられ、サービス側のタイムアウト 	リスクを低減できます。その後は、更新対象期間のみに限定した通常の増分更新が適用されるため、安定した運用が可能になります。
</br>

## 前提条件
ライセンス：XMLA エンドポイントを使用するには、Premium 容量、Premium Per User (PPU)、または Microsoft Fabric 容量 に割り当てられたワークスペースが必要です。
テナント設定：「XMLA の読み取り/書き込み」を有効にする必要があります。
> [!TIP]
[Power BI での XMLA エンドポイントを使用したセマンティック モデルの接続と管理 - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-premium-connect-tools#enable-xmla-read-write)

</br>

## 手順：初回更新を手動で実行する方法

### 1. 増分更新を設定し、Power BI サービスに発行（ただし更新は行わない）
Power BI Desktop 上で増分更新を設定し、Power BI サービスに発行します。
設定方法は以下のブログを参照してください。
[増分更新の概要と設定方法 | Japan CSS Support Power BI Blog](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_incremental_refresh/)
この時点では Power BI サービス上での更新は実行しません。更新を行うと保持期間全体が一括で処理されるため、更新を行うとタイムアウトが発生する可能性があります。後続の XMLA エンドポイント更新に備えて、あくまで発行のみを行います。
</br>

### 2. ワークスペースの XMLA エンドポイントを取得
Power BI サービスの対象ワークスペースを開き、以下の手順で XMLA エンドポイントをコピーします。
[ワークスペースの設定] → [プレミアム] タブ → [接続リンク] → [コピー]
<div align="left">
<img src="1.png">
</div>
</br>

### 3. Tabular Editor でセマンティックモデルに接続し、パーティションを作成
> [!TIP]
TIPS：Tabular Editor は、表形式モデルを直感的に管理できる外部ツールです。
Tabular Editor の詳細は、以下の公式サイトをご参照ください。
[Releases · TabularEditor/TabularEditor](https://github.com/TabularEditor/TabularEditor/releases)
[Tabular Editor | Tabular Editor Documentation](https://docs.tabulareditor.com)
※サードパーティ製ツールのため、Microsoft によるサポートは提供されていません。

①	 Tabular Editor を起動し、[File] > [Open] > [From DB] を選択します。
<div align="left">
<img src="2.png">
</div>

②	ステップ 2 で取得した XMLA エンドポイントと資格情報を入力し、ワークスペースに接続します。
<div align="left">
<img src="3.png">
</div>

③	設定対象のセマンティックモデルを選択します。
<div align="left">
<img src="4.png">
</div>

④	増分更新が設定されたテーブルを右クリックし、[Apply Refresh Policy] を選択します。
[What is a Refresh Policy? | Tabular Editor Documentation](https://docs.tabulareditor.com/te3/tutorials/incremental-refresh/incremental-refresh-about.html?tabs=filterstep%2Cimport)
<div align="left">
<img src="5.png">
</div>

⑤	以下のように、保持期間に基づく複数のパーティションが自動で作成されます。
![](6.png)
<div align="left">
<img src="6.png">
</div>

### 4. SSMS からパーティションを更新
①SSMS を起動し、Server type を「Analysis Services」に設定して XMLA エンドポイントに接続します。
<div align="left">
<img src="7.png">
</div>

②対象のセマンティックモデルを展開し、該当テーブルを右クリックして [Partitions] を選択します。
<div align="left">
<img src="8.png">
</div>

③自動作成された複数のパーティションが表示され、[Last Processed] が「Never」になっていることを確認します。
パーティションを更新するには、緑色の [Process] ボタンを押します。
<div align="left">
<img src="9.png">
</div>

④更新対象のパーティションを選択する画面が表示されます。ここで複数のパーティションを段階的に処理することで、
初回更新のタイムアウトを回避できます。GUI 操作だけでなく、XMLA クエリによる処理も可能です。
※この例ではすべてのパーティションを一括処理しましたが、大量のデータを処理する場合は、パーティションは個別にもしくは少数単位で分割して処理することもできます。
<div align="left">
<img src="10.png">
</div>

⑤処理が完了すると、完了メッセージが表示されます。
<div align="left">
<img src="11.png">
</div>

⑥ [Last Processed] の日時が更新されたことを確認します。
<div align="left">
<img src="12.png">
</div>
</br>

### 5. Power BI サービス上で更新
① Power BI サービスのワークスペース上で「今すぐ更新」を実行します。保持期間のパーティションがすでに処理済みであるため、更新期間のパーティションのみが処理対象になります。 
<div align="left">
<img src="13.png">
</div>

② 更新後、SSMS で再度確認すると、[Last Processed] の日付が更新期間のパーティションにだけ反映されていることが確認できます。
※本件では過去7日分を増分更新の対象としております
<div align="left">
<img src="14.png">
</div>
</br>

## おまけ：少量データでセマンティックモデルを発行する方法
本番データのボリュームが大きい場合、初回発行時にアップロードが完了するまでに時間がかかることがあります。
また、Premium 容量をご利用の場合でも、Power BI Desktop からの発行時には 10GB のファイルサイズ上限があるため、大規模なデータモデルではアップロード自体が失敗する可能性もあります。
このようなケースを回避するために、初回は意図的に「データ量を極力抑えた状態」でセマンティックモデルを発行し、その後に運用構成へ切り替える方法が有効です。以下に代表的な 2 つの手法を紹介します。

### 1.Power Query で事前にデータを除外し、発行後に ALM Toolkit でフィルターを削除する
Power BI Desktop 上でモデルを作成する際、Power Query に一時的なフィルター（例：少数行だけ残す、もしくは全件除外）を追加し、発行時のデータ量を最小限に抑えます。その後、ALM Toolkit を使ってフィルター条件を削除すれば、本来の構成に復元可能です。これにより、初回発行時の負荷を回避しつつ、構造を維持したまま運用データへ切り替えることができます。
詳細な手順は以下の公式ドキュメント・動画をご参照ください。
[Power BI での XMLA エンドポイントを使用した高度な増分更新およびリアルタイム データ - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/connect-data/incremental-refresh-xmla#power-query-filter-for-empty-partitions)
[Deploy Power BI dataset schema changes WITHOUT refreshing! - YouTube](https://www.youtube.com/watch?v=s0j6d3UAw9U)
<br>

### 2.同じスキーマのテストデータに接続し、パラメーターを使って接続先を切り替える
開発時には、本番環境と同じスキーマ構造を持つテスト用の軽量データソースに接続し、接続先を切り替えるためのパラメーターを作成します。Power BI サービスに発行した後、データの更新を行う前にパラメーターの値を編集し、本番環境のデータソースに切り替えることができます。
詳細な手順は以下のブログをご参照ください。
[Power BIにおけるデータソースのパラメーター化 | Japan CSS Support Power BI Blog](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_datasource_parameter/)
<br>


以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。
<br>

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)