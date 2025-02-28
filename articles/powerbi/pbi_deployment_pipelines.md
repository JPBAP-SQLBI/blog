---
title: デプロイパイプラインについて
date: 2025-02-28 00:00:00 
tags:
  - Power BI
  - Microsoft Fabric
  - Power BI サービス
  - デプロイパイプライン
  - 配置パイプライン
  - Deployment pipelines
  - deployment rules

---

こんにちは、Power BI サポート チームの中川です。

Power BI では、デプロイパイプライン（配置パイプライン）を利用することで、レポートの開発・テスト・本番環境への展開をスムーズに管理することができます。
また、配置ルールを利用することで、ステージごとに異なるデータソースを設定できるため、開発ステージではダミーデータを使用し、テストや本番ステージでは本番に近いデータを用いた検証が可能になります。
これにより、本番環境への影響を抑えたレポートの修正・テストを行うことができ、品質の向上と運用の効率化を図ることができます。
 
本ブログでは、 SQL Server を例に、開発・テスト環境で異なるデータを取得する方法を中心に、デプロイパイプラインの利用方法についてご紹介いたします。


<!-- more -->
> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
## 目次
---
* [デプロイパイプラインについて](#デプロイパイプラインについて)
* [前提条件・制限事項](#前提条件・制限事項)
* [配置ルール作成手順 データソースの規則](#配置ルール作成手順-データソースの規則)
* [配置ルール作成手順 パラメーターの規則](#配置ルール作成手順-パラメーターの規則)
* [おわりに](#おわりに)


---
## デプロイパイプラインについて
---
デプロイパイプラインは、既定では開発（Development）、テスト（Test）、本番（Production）の 3つのステージを基にして作業を行います。各ステージはワークスペースに紐づけられており、必要に応じてステージを追加、削除することも可能です。ステージ数は 2 個から 10 個に設定できます。

### 特徴
デプロイパイプラインには以下のような特徴があります。

- 簡単なデプロイ操作  
  - ボタン操作で各ステージ間のコンテンツのコピーや差分の確認が可能です。
- 配置ルールの設定  
  - 各ステージで異なるデータソースを設定できるため、環境ごとに動作を検証できます。
- デプロイ履歴  
  - デプロイ履歴からデプロイ先や日時、項目などが確認できます。

### アイテムペア設定
アイテムペア設定とは、デプロイパイプラインの 1つのステージにあるアイテムを、隣接するステージにある同じアイテムと関連付けるプロセスです。アイテムペア設定を行う操作をペアリングと呼びます。
意図しない重複やデプロイの失敗を防ぐためには、ペアリングの仕組みを理解することが重要になりますので簡単に紹介します。
 
#### ペアリングのポイント
- 手動でペアリングはできない  
  - 自動的にペアリングが行われます。  
  - [ペアリングの規則](https://learn.microsoft.com/ja-jp/fabric/cicd/deployment-pipelines/assign-pipeline?tabs=new-ui#pairing-rules)に従う以外は、項目を手動でペアリングする方法はありません。
- 名前変更してもペアリングは解除されない  
  - ペアリングされたアイテムは、名前を変更してもペアのままです。  
  - そのため、異なる名前でもペアリングされている場合があります。
- ペアリングされていないアイテムは単独で表示される  
  - ペアリングされていない場合、同じ名前・種類でも重複してコピーされ、単独の行として表示されます。

以下は、開発ステージとテストステージで、それぞれのセマンティックモデルをもとに新規にレポートを作成した場合の、テストステージの画面です。
下から2行はペアリングされていないため、単独の行として表示されています。


<div align="center">
<img src="Paired_items_Report_with_each_development_test.png">
</div>

</br>
どのような状況でアイテムがペアリングされるかについては、以下のリンクをご参照ください。

>[!NOTE]
> 参考情報：[展開パイプラインにワークスペースを割り当てる - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/cicd/deployment-pipelines/assign-pipeline?tabs=new-ui#item-pairing)


### 新しいＵＩ
現在は新しいユーザーインターフェイス（UI）が利用可能となっています。新しい UI は元の UI と機能は同じであり、元の UI でできることは、新しい UI でも行うことができます。
 
新しい UI の主な変更点として、ステージを選択するとそのステージに関連するすべての操作を一箇所で行えるようになっています。また、デプロイ対象のアイテムを検索、フィルター、ソートする機能などが含まれています。
 
本記事では、新しい UI を使用して操作をご紹介しています。ただし、新しい UI は現在プレビュー段階のため、動作に不具合等が生じる可能性があります。その場合は、旧 UI に戻して試していただくことを推奨します。

>[!NOTE]
> 参考情報：[Fabric 展開パイプラインの新しいユーザー インターフェイスの概要 - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/cicd/deployment-pipelines/deployment-pipelines-new-ui)


---
## 前提条件・制限事項
---
デプロイパイプラインではいくつかの前提条件や制限事項がございます。



### 要件
デプロイパイプラインを作成・管理するには、以下の条件を満たす必要があります。
-	Fabric 容量 または Premium ライセンス（Per Capacity または Per User）を所有していること
-	Fabric ワークスペースの管理者 であること
 
### サポートされているアイテム
デプロイパイプラインでデプロイ可能なコンテンツには、レポート、ダッシュボード、セマンティックモデルの他にも、 Fabric アイテムも含まれます。
 
現在、 Fabric アイテムの多くはプレビュー段階にあります。
プレビュー機能は今後変更される可能性があるため、利用時には注意いただきますようお願いいたします。

>[!NOTE]
> 参考情報：[Fabric デプロイ パイプラインの概要 - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/cicd/deployment-pipelines/intro-to-deployment-pipelines?tabs=new-ui#supported-items)


### デプロイ時にコピーされるデータ
デプロイ時には、レポートのビジュアルやデータソース（配置ルール）の定義などのメタデータがコピーされますが、実際のデータや資格情報はコピーされません。
そのため、各ステージで適切なデータソースへの接続設定と更新を行う必要があります。


>[!NOTE]
> 参考情報：[Microsoft Fabric デプロイ パイプライン プロセス - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/cicd/deployment-pipelines/understand-the-deployment-process?tabs=new-ui#item-properties-copied-during-deployment)



---
## 配置ルール作成手順 データソースの規則
---

本セクションでは、デプロイパイプラインを作成した後の配置ルール「データソース規則」を設定する方法についてご紹介いたします（手順 7 - デプロイ規則を作成する）。
前提として、以下の公開情報の手順 1～6 までの別のステージにコンテンツにデプロイが完了している状態を想定しています。
手順 1～6 の詳細については、公開情報をご確認ください。
 
>[!NOTE]
> 参考情報：[展開パイプライン (Fabric のアプリケーション ライフサイクル管理 (ALM) ツール) の使用を開始する - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/cicd/deployment-pipelines/get-started-with-deployment-pipelines?tabs=from-fabric%2Cnew-ui)

### 前提となる環境
デプロイパイプラインの「データソース規則」 を設定することで、各ステージ（開発、テスト）で異なるデータソース を使用します。

本手順では、以下の環境を想定しています。
サーバー名とデータベースが異なり、スキーマ名とテーブル名が同一です。

| ステージ | サーバー名 | データベース名 | スキーマ名 | テーブル名 |
|----------|------------------------------------------------|--------------------------|-----------|------------|
| 開発     | deployment-pipelines-server-__dev__.database.windows.net | deployment-pipelines-db-__dev__  | salesLT   | salesData  |
| テスト   | deployment-pipelines-server-__test__.database.windows.net | deployment-pipelines-db-__test__ | salesLT   | SalesData  | 


データの違いは以下の通りです。

開発データ

| SalesID | ProductName      | Quantity | SalesDate  |
|---------|-----------------|----------|------------|
| 1       | __Test__ Product A  | 10       | 2025-01-01 |
| 2       | __Test__ Product B  | 20       | 2025-01-02 |

テストデータ

| SalesID | ProductName      | Quantity | SalesDate  |
|---------|-----------------|----------|------------|
| 1       | __Real__ Product A  | 100      | 2025-01-01 |
| 2       | __Real__ Product B  | 200      | 2025-01-02 |
| 3       | __Real__ Product C  | 300      | 2025-01-03 |
| 4       | __Real__ Product D  | 400      | 2025-01-04 |


### 開発のステージのレポートと各ステージのパイプライン

開発ステージのレポート

<div align="center">
<img src="Before_report_modification_test.png">
</div>

開発ステージのパイプライン

<div align="center">
<img src="Deploy_screen_dev.png">
</div>


テストステージのパイプライン

<div align="center">
<img src="Deploy_screen_test.png">
</div>


作成手順
1. テストステージへアクセス  
   a. Power BI サービスにアクセスし、対象のデプロイパイプラインを開く。  
   b. テストステージを開く。  

2. 配置ルールの設定を開く  
   a. テストステージの「配置ルール」ボタンをクリック。  
   b. 対象のセマンティックモデルを選択。  

3. データソース規則の作成  
   a. 「データソースの規則」を選択。  
   b. 「規則の追加」ボタンをクリックして、新しいルールを作成。  

4. テストステージ用のデータソースを設定  
   a. テストステージ用のサーバー名とデータベース名を設定し、保存する。  
    <div align="left">
    <img src="Deployment_Rules.png" width="70%">
    </div>

5. コンテンツの再デプロイ  
   a. 開発ステージからテストステージへ再デプロイする。  

6. テストステージの資格情報の設定  
   a. テストステージのセマンティックモデルの資格情報を確認。  
   b. 次のようなメッセージが表示されている場合、テストステージ用の資格情報を設定する。  
      *「データソースへの接続をテストできませんでした。資格情報をもう一度お試しください。」*  
      <div align="left">
      <img src="Credentials_error_after_deployment_rule_expansion.png" width="80%">
      </div>

7. セマンティックモデルの更新と動作確認  
   a. テストステージのセマンティックモデルを更新して、データを取得。  
   b. テストステージのレポートが、テストステージ用のデータを反映していることを確認。  
    <div align="left">
    <img src="After_report_modification_test.png">
    </div>


なお、配置ルールでサポートされているデータソース については、以下のリンクを参照してください。
 

>[!NOTE]
> 参考情報：[サポートされているデータ ソース - Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/cicd/deployment-pipelines/create-rules?tabs=new-ui#supported-data-sources-for-dataflow-and-semantic-model-rules)

---
## 配置ルール作成手順 パラメーターの規則

前のセクションではサーバー名とデータベース名が異なる場合の例を紹介しましたが、スキーマ名やテーブル名が異なるケースもあります。本セクションでは、その場合の対応方法を紹介します。

以下のように、 スキーマ名とテーブル名も異なる状況を想定します。

| ステージ | サーバー名 | データベース名 | スキーマ名 | テーブル名 |
|----------|------------------------------------------------|--------------------------|-----------|------------|
| 開発     | deployment-pipelines-server-__dev__.database.windows.net | deployment-pipelines-db-__dev__  | __dev__   | __salesDataDev__ |
| テスト   | deployment-pipelines-server-__test__.database.windows.net | deployment-pipelines-db-__test__ | __test__   | __SalesDataTest__  |

 
デプロイパイプラインでは「パラメーター規則」が使用できますので、 Power BI Desktop でパラメーターを作成し、詳細エディターでそのパラメーターを参照するように修正します。
 
なお、 Power BI でのパラメーターの作成方法の詳細は以下のブログをご参照ください。

>[!NOTE]
> 参考情報：[Power BIにおけるデータソースのパラメーター化 | Japan CSS Support Power BI Blog](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_datasource_parameter/)


 
以下は、作成したパラメーターと詳細エディターの画面です。

 __[注意] パラメーターの規則を使う場合、パラメーターが Text型である必要があります。__

<div align="left">
<img src="Parameters.png">
</div>

<br>

<div align="center">
<img src="Parameters_Schema_Table_Name_Detail_Editor.png">
</div>


パラメーターの作成完了後、開発ステージへの発行、テストステージへデプロイし、デプロイパイプラインのテストステージの「配置ルール」から「パラメーターの規則」を次のように設定します。

  <div align="left">
  <img src="Deployment_Parameter_Rules.png">
  </div> 
 
<br>
なお、これら以外の手順は「データソースの規則」と同様のため割愛します。

---
## おわりに
この記事では、デプロイパイプライン（配置パイプライン）の概要と、配置ルールの作成手順についてご説明しました。
 
デプロイパイプラインを利用することで、異なる環境間での一貫性を保ったデプロイが可能となり、手動操作のミスを減らすことができます。また、配置ルールを活用することで、環境ごとの設定を柔軟に管理できるため、効率的な開発・テスト・本番運用が実現できます。
本ブログが皆様の業務効率化にお役立ていただければ幸いです。
 
以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。


---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)