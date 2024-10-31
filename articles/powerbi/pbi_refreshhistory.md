---
title: セマンティック モデルの更新履歴を REST API で取得する方法
date: 2024-09-30 00:00:00
tags:
 - Power BI
 - Power BI サービス
 - Power BI Desktop
 - REST API
 - 更新
 - 更新履歴
 - refresh
 - refresh history
--- 


こんにちは、 Power BI サポート チームの山下です。  
多くのユーザー様から、Power BI サービス上のセマンティック モデルの更新履歴（更新開始時間、終了時間、成否結果など）を一括で取得したいというお問い合わせをいただきます。  
画面上では、個々のセマンティック モデルの更新履歴画面から確認することが可能ですが、セマンティック モデルの数が多い場合、手作業での確認は非常に大変です。  
そこで、本記事では、REST API を使用して、ユーザーが権限をもつワークスペースに存在するセマンティック モデルの更新履歴を一括で取得する方法をご紹介します。  
この方法を使用することで、作業の効率化、時間の節約にもつながりますので、状況に応じてぜひご活用ください。    

 </br>

<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。


 </br>

##  <font color="DodgerBlue">“Get Refresh History In Group”の利用方法</font>      

セマンティック モデルの更新履歴更新開始時間・終了時間・成否結果などの情報につきましては、GUI 以外では “Get Refresh History In Group” という Power BI REST API にて取得可能です。  
ただし、API を実行するアカウントが対象のセマンティック モデルに対して読み取り権限を持っていることが前提条件となります。  
グローバル管理者や Fabric 管理者（ Power BI 管理者）であっても、対象のセマンティック モデルに対して読み取り権限を持たない場合は情報取得することができませんことを予めご了承ください。    
ご参考情報：    
[Datasets - Get Refresh History In Group](https://learn.microsoft.com/ja-jp/rest/api/power-bi/datasets/get-refresh-history-in-group)    
 </br>
 
こちらの公式ドキュメントの［▷使ってみる］をクリックすると画面右側にフォーカスモードが開始されます。  
Power BI サービスを使用するアカウントでサインイン後、API の動作をお試しいただけます。  

<div align="left">
<img src="1.png">
</div>

 </br>
以下は “Get Refresh History In Group” の実行結果の例となります。   

＝＝　実行結果例　（ UTC 時間となりますので、日本時間と 9 時間のずれが生じます。）＝＝  

```
 {
      "requestId": "40935061-9857-41c9-a684-8bc97b4cbc7e",
      "id": 317934293,
      "refreshType": "Scheduled",　<-- 更新の種類
      "startTime": "2024-08-15T04:30:25.867Z",　　<-- 更新開始時間
      "endTime": "2024-08-15T04:30:30.88Z",　　　<-- 更新終了時間
      "status": "Completed",　　　<--　更新の成否の結果　
      "refreshAttempts": [　　＜-- これ以降は、より詳細な更新処理内容の情報となります。※1
        {
          "attemptId": 1,
          "startTime": "2024-08-15T04:30:26.225194Z",
          "endTime": "2024-08-15T04:30:30.6002893Z",
          "type": "Data"
        },
        {
          "attemptId": 1,
          "startTime": "2024-08-15T04:30:30.7252936Z",
          "endTime": "2024-08-15T04:30:30.8034226Z",
          "type": "Query"
```

//　該当の更新履歴（ GUI ）  
<div align="left">
<img src="2.png">
</div>

 </br>

※１　ご参考情報：  

[セマンティック モデルの更新履歴](https://learn.microsoft.com/ja-jp/power-bi/connect-data/refresh-data#semantic-model-refresh-history)    

＊　関連箇所抜粋  ＊  
Power BI 更新の試行はそれぞれ 2 つの操作に分けられます。  
**データ** – セマンティック モデルにデータを読み込む　　
**クエリ キャッシュ** – Premium クエリ キャッシュやダッシュボード タイルの更新


### <font color="HotPink">groupId と datasetId の指定</font> 
本 API では、対象のセマンティック モデルの groupId と datasetId を指定する必要がございます。  
groupId と datasetId は、Web ブラウザで Power BI サービスにサインインし、対象のセマンティック モデル画面を開いた際のアドレスバーに表示されるURLからご確認いただけますが、以下 API を使用することで、一括で情報を取得することも可能です。  

https : // app.powerbi.com/groups/ <font color="HotPink">groupId </font>/datasets/ <font color="HotPink">datasetId</font> /details?experience=power-bi  


<div align="left">
<img src="3.png">
</div>


ご参考情報：  
[Admin - Datasets GetDatasetsAsAdmin](https://learn.microsoft.com/ja-jp/rest/api/power-bi/admin/datasets-get-datasets-as-admin) 
テナント内に存在するデータセットの一覧を返します。
[Datasets - Get Datasets In Group](https://learn.microsoft.com/ja-jp/rest/api/power-bi/datasets/get-datasets-in-group) 
指定したワークスペースからデータセットの一覧を返します。

上記をおまとめいたしますと、① “Datasets GetDatasetsAsAdmin” や Get Datasets In Group” の API の実行結果から各セマンティック モデルの groupId と datasetId を取り出し、② その情報をもとに Get Refresh History In Group“ を実行するようなスクリプトを作成いただくことで、読み取り権限をもつセマンティック モデルのスケジュール更新の更新履歴を一括で取得することが可能になります。  
 </br>

##  <font color="DodgerBlue"> Power BI Desktop から直接 REST  API の実行結果を取得する方法</font>    

Power BI Desktop から直接 REST API の実行結果を取得する方法として、「PowerBIRESTAPI」というカスタムコネクタを利用する方法があります。  

ご参考情報：  
[PowerBIRESTAPI](https://github.com/migueesc123/PowerBIRESTAPI)   

※なお、本カスタムコネクタ は Microsoft が開発しているものではないため、コネクタ自体の動作に関して問題が生じた場合弊社でご支援することが難しいです。　　
ご利用の際は貴社にて十分に検証・検討を実施いただきますようお願いいたします。　　

 </br>

### <font color="HotPink">カスタム コネクタの利用方法</font> 　　

1. 上記 github のサイトから取得したコネクタの .mez ファイルをローカルの [ ドキュメント ]\Microsoft Power BI Desktop\Custom Connectors フォルダーに入れてください。  
フォルダーが存在しない場合は、ローカルにて上記のフォルダーを作成します。　　

2. データ拡張機能のセキュリティ設定を調整するため、Power BI Desktop で、[ファイル] > [オプションと設定] > [オプション] > [セキュリティ] の順に展開ください。 

3.  [データ拡張機能 から [(非推奨) 検証または警告せずに、あらゆる拡張機能の読み込みを許可する] を選択ください。　　

4. [OK] を選択して、Power BI Desktop を再起動ください。  

※ Power BI Desktop のデータ拡張機能の既定のセキュリティ設定は、[(推奨) Microsoft 認定の拡張機能と他の信頼されたサード パーティー製の拡張機能のみの読み込みを許可する] です。  
今回ご紹介しているカスタムコネクタは、認定されていないカスタムコネクタとなっているため、上記設定が必要となります。  

 
5. その後、[データを取得] から [詳細] を展開いただき、Power BI API (ベータ) (カスタム)を選択し、接続ください。  

<div align="left">
<img src="4.png">
</div>

6. REST API を実行する Entra ID アカウントでサインインを行い、接続ください。  

<div align="left">
<img src="5.png">
</div>

7. その後、表示されますナビゲーター画面にて [Workspaces] を展開いただき、[Refresh History] をご確認ください。  
サインインしたアカウントが権限をもつセマンティック モデルの、Workspace ID、Dateset ID、更新開始時間と終了時間および成否等の情報を一括で取得することが可能になります。  


<div align="left">
<img src="6.png">
</div>


カスタムコネクタ の詳細については、以下の公開情報に説明がございます。  
ご参考情報：  
[Power BI でのコネクタの機能拡張](https://learn.microsoft.com/ja-jp/power-bi/connect-data/desktop-connector-extensibility) 


</br>
以上、本ブログ が少しでも皆様のお役に立てますと幸いでございます。  

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)