---
title: Power BIにおけるデータソースのパラメーター化
date: 2023-07-31 00:00:00 
tags:
  - Power BI
  - パラメーター
  - Power Query
---
こんにちは、Power BI サポート チームの呂です。
Power BI では、Power Queryのパラメーターを活用して、データセットのデータソースを動的に変更する方法があることをご存知ですか。パラメーターを使ってデータソースに接続し、パラメーターを編集することで、データソースを必要に応じて簡単に変更できます。これにより、異なる要件に対応する柔軟性を持ったレポートを作成し、レポートの再利用性と拡張性を向上させられます。
今回の記事では、SQL Serverを例に、データソースのパラメーター化の設定方法をご紹介いたします。

<!-- more -->
> [!IMPORTANT]  
> 本記事編集時点と実際の機能に相違がある場合がございます。予めご了承ください。
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
## 目次
---
1. [データソースのパラメーター化の応用例](#データソースのパラメーター化の応用例)
2. [データソースのパラメーター化設定手順](#データソースのパラメーター化設定手順)
3. [パラメーターの変更方法](#パラメーターの変更方法)
4. [Excelデータソースの場合](#Excelデータソースの場合)
4. [パラメーターを適用した場合の動作](#パラメーターを適用した場合の動作)
</br>

---
## データソースのパラメーター化の応用例
---

・開発／テスト／本番など異なるデータソース環境の間で簡単に切り替えたい場合
・部門や地域ごとに異なるデータソースを使用している場合
・Power BI Serviceに発行されたデータセットのデータソースを切り替えたい場合
<br>

---
## データソースのパラメーター化設定手順
---
※今回検証を行った環境では、１つのサーバーに「Northwind」と「test」という２つのデータベースを用意しています。

<div align="left">
<img src="1.png">
</div>

１．データソースのパラメーターを設定する前に、まずはPower Queryエディターの[表示]タブで、パラメーターの[常に許可]にチェックを入れます。

<div align="left">
<img src="2.png">
</div>

設定後は以下のように、データソースに接続する際に、固定の接続先だけでなく、サーバー名やデータベース名のパラメーターで作成し、設定可能になります。

<div align="left">
<img src="3.png">
</div>

２．SQL Serverの接続画面から[新しいパラメーター]を選択し、サーバー名やデータベース名のパラメーターを設定します。
<div align="left">
<img src="4.png">
</div>
※パラメーターの[種類]が[すべて]に設定されている場合、Power BI サービスでパラメーターを編集できない可能性がございますため、[テキスト]もしくは[10進数]に設定していただく必要がございます。

> [!TIP]
> 参考事例：[Parameter is disabled for editing in power bi service - Microsoft Fabric Community](https://community.fabric.microsoft.com/t5/Service/Parameter-is-disabled-for-editing-in-power-bi-service/m-p/398733)

３．設定されたパラメーターを使って、SQL Serverデータベースに接続します。

<div align="left">
<img src="5.png">
</div>

以上で、データソースのパラメーター化設定が完了です！

<br>

---
## パラメーターの変更方法
---

### Power BI Desktopの場合
１．[ホーム]タブの[データの変換]より、[パラメーターの編集]を選択します。

<div align="left">
<img src="6.png">
</div>

２．ポップアップ画面から、データソースのパラメーターを変更できます。
※以下例では、データベース名のパラメーターを「Northwind」を「test」に変更しました。

<div align="left">
<img src="7.png">
</div>
<br>

### Power BI サービスの場合
１．ワークスペースから、データセットの[・・・]＞[設定]を選択します。

<div align="left">
<img src="8.png">
</div>

２．設定画面の[パラメーター]から、データソースのパラメーターを変更できます。

<div align="left">
<img src="9.png">
</div>

> [!TIP]
> 参考情報：[Power BI サービスのパラメーター設定を編集する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/connect-data/service-parameters)
<br>
<br>

---
## Excelデータソースの場合
---

本記事の前半では、接続時にデータソースのパラメーター化する方法をご紹介しましたが、実は、データソースのパラメーターは必ずしも接続時に設定する必要がなく、接続後にも[詳細エディター]より設定可能です。
例えば、Excelファイルの場合、接続時に特定の Excel ファイルをデータソースとして指定する必要がありますため、SQL Serverのように、接続画面からデータソースのパラメーターを設定できません。
その場合、Excelファイルへ接続後にパラメーターを設定することができますので、以下の例にて説明します。

１．[UFO_US.xlsx]というExcelファイルに接続しますと、[詳細エディター]では以下のように表示されます。

```m
let
    ソース = Excel.Workbook(File.Contents("C:\Users\lyuyue\Documents\UFO_US.xlsx"), null, true),
    UFO_US_Sheet = ソース{[Item="UFO",Kind="Sheet"]}[Data],
    昇格されたヘッダー数 = Table.PromoteHeaders(UFO_US_Sheet, [PromoteAllScalars=true]),
    変更された型 = Table.TransformColumnTypes(昇格されたヘッダー数,{{"datetime", type text}, {"city", type text}, {"state", type text}, {"country", type text}, {"shape", type text}, {"duration (seconds)", type number}, {"duration (hours/min)", type text}, {"comments", type text}, {"date posted", type date}, {"latitude", type number}, {"longitude ", type number}})
in
    変更された型
```

２．Power Query エディターの[ホーム]＞[パラメーターの管理]＞[新しいパラメーター]を選択します。

<div align="left">
<img src="10.png">
</div>

３．Excelファイルのファイルパス変更用のパラメーターを作成します。

<div align="left">
<img src="11.png">
</div>

４．[詳細エディター]を開き、２行目のありましたファイルパスの部分をパラメーター名に差し替えます。

```m
let
    ソース = Excel.Workbook(File.Contents(ファイルパス), null, true),
    UFO_US_Sheet = ソース{[Item="UFO",Kind="Sheet"]}[Data],
    昇格されたヘッダー数 = Table.PromoteHeaders(UFO_US_Sheet, [PromoteAllScalars=true]),
    変更された型 = Table.TransformColumnTypes(昇格されたヘッダー数,{{"datetime", type text}, {"city", type text}, {"state", type text}, {"country", type text}, {"shape", type text}, {"duration (seconds)", type number}, {"duration (hours/min)", type text}, {"comments", type text}, {"date posted", type date}, {"latitude", type number}, {"longitude ", type number}})
in
    変更された型
```

５．パラメーターの設定後は以下のように、接続先のファイルパスを変更することが可能になります。

<div align="left">
<img src="12.png">
</div>
<br>
<br>

---
## パラメーターを適用した場合の動作
---

最後にExcelのサンプルファイルでのパラメーターを変更し、適用した動作についてご紹介します。
以下の通り、[ファイルパス]のパラメーターを編集することで、データソースを「US」と「US以外」のファイル間で、必要に応じて切り替え可能です。
同様のスキーマのデータソースが複数存在し、切り替えが必要である場合はぜひこの方法をご活用ください。

<div align="left">
<img src="13.png">
</div>

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。
<br>

---
### 参考情報
---
-  [公開情報：パラメーター クエリを作成する (Power Query)](https://support.microsoft.com/ja-jp/office/%E3%83%91%E3%83%A9%E3%83%A1%E3%83%BC%E3%82%BF%E3%83%BC-%E3%82%AF%E3%82%A8%E3%83%AA%E3%82%92%E4%BD%9C%E6%88%90%E3%81%99%E3%82%8B-power-query-5eb365bc-3982-4ab2-8830-b205a69e0f33)
-  [外部情報：How to Parameterize Data Sources in Power BI | phData](https://www.phdata.io/blog/how-to-parameterize-data-sources-power-bi/)
-  [外部情報：Parameterize your data source! – Data – Marc](https://data-marc.com/2018/11/15/parameterize-your-data-source/)
-  [ビデオ：Making data source parameters easy in Power BI Desktop - Guy in a Cube](https://www.youtube.com/watch?v=OnaDJkGOmIE)

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)