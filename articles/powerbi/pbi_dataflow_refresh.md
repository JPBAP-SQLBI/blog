---
title: データフローの更新方法
date: 2025-07-31 00:00:00 
tags:
  - Power BI
  - Power BI サービス
  - データフロー
  - 更新
  - Refresh
---

# データフローの更新方法

こんにちは、Power BI サポート チームの亀田です。

Power BI / Mircrosoft Fabric で利用できる ETL ツールであるデータ フローは、現在データフロー Gen1、データフロー Gen2の2つを利用することができます。通常、スケジュールで更新を行うことが多いですが、今回はそれぞれのデータフローの更新方法について説明します。

<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、　　
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

## 目次

* [データフローとは](#データフローとは)
* [リンク データフロー](#リンク-データフロー)
* [データフローの更新方法](#データフローの更新方法)
    * [オンデマンド更新](#オンデマンド更新)
    * [スケジュール更新](#スケジュール更新)
    * [REST API](#REST-API)
    * [Data Factory の Pipeline](#Data-Factory-の-Pipeline)
    * [Power Automate](#Power-Automate)
* [おわりに](#おわりに)

## データフローとは

データフローは、データの接続や変換ができる Power BI アイテムです。Power BI で利用できていたデータフローは、データフロー Gen1 とよばれ、Microsoft Fabric が登場した際に追加された新しいデータフローはデータフロー Gen2 とよばれています。データフロー Gen1 / Gen2 はアーキテクチャも異なっており、現在はどちらのデータフローも利用することができるようになっています。

データフロー Gen2 ではいくつかの機能が追加されていますが、その中の1つの機能としてレイクハウスやウェアハウスなどへの同期もできるようになりました。同期を設定することで、データフローを更新したとき同時にレイクハウス等の格納先のアイテムに変換後のデータを取り込むことができます。

> [!NOTE]
> [データフロー Gen1 とデータフロー Gen2 の違い - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/data-factory/dataflows-gen2-overview)
> [Power BI データフロー Gen2 と Gen1 の比較 | Japan CSS Support Power BI Blog](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_dataflow_gen1_gen2/)

<div align="center">
<img src="dataflow_refresh_01.png">
</div> 

データフローは Power Apps でも利用できますが、今回は Power BI で利用するデータフローを前提として更新方法について説明します。

## リンク データフロー

更新の動作の説明に関して、データフローで利用できるリンク テーブルについて取り上げます。リンク テーブルは、Power  BI Premium / Fabric 容量で利用できる機能であり、データフロー内でほかのデータフローのテーブルを参照することでリンクされます。

> [!NOTE]
> [データフロー間でテーブルをリンクする - Power Query | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-query/dataflows/linked-tables)

データフローのリンク テーブルを利用することのメリットは、すでに利用されたテーブルを参照することで、同じデータ ソースに対して繰り返し更新する必要がないことです。変換済みのデータを参照するため更新時間を短縮することができるほか、参照しているデータはすべて同じであることが保証されるため、データソースは同じであっても更新タイミングによってデータが異なり表示しているデータが異なるといったことを避けることができます。

また、リンク テーブルを利用する場合、同じワークスペース内に参照するデータフローが存在している場合には更新が連動します。参照元のデータフローを更新することで参照しているデータフローのテーブルも**自動で更新されます**。参照元のデータフローを更新後に参照しているデータフローの更新をスケジュールしたりする必要がないというのはメリットになります。本動作はデータフロー Gen1 のみ適用され、データフロー Gen2 は同様の動作にはなりません。

<div align="center">
<img src="dataflow_refresh_02.png">
</div> 

リンク テーブル以外のテーブルは自動で更新されず、スケジュール更新を設定する必要がありますのでご注意ください。

## データフローの更新方法

データフローについては、先ほど取り上げたとおり現在データフロー Gen1、データフロー Gen2 が利用できます。このうちデータフロー Gen2 では、最近継続的インテグレーションと継続的デプロイ (CI/CD) と Git 統合をサポートするデータフロー Gen2 が GA (一般公開) となりました。この機能を有効化した場合には、通常のデータフロー Gen2 とは機能上の制限がありますので別に取り上げ、本記事ではデータフロー Gen1 / データフロー Gen2 / データフロー Gen2 CI/CD の3つのデータフローについて更新の動作について説明します。

> [!NOTE]
> [CI/CD と Git 統合を使用する Dataflow Gen2 - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/data-factory/dataflow-gen2-cicd-and-git-integration)

今回取り上げる更新方法はオンデマンド更新、スケジュール更新、REST API、Data Factory の Pipeline、Power Automate の 4 つです。それでは、実際に更新の方法を見てみます。

### オンデマンド更新

データフロー Gen1 / Gen2 ともにワークスペース上でデータフローにマウスオーバーした際に表示される [今すぐ更新] から更新を行うことができます。

<div align="center">
<img src="dataflow_refresh_03.png">
</div> 

データフロー Gen2 CI/CD では、上記のメニューは表示されず、[その他のオプション] > [今すぐ更新] から更新を行います。

<div align="center">
<img src="dataflow_refresh_04.png">
</div> 

### スケジュール更新

データフロー Gen1 / Gen2 ともに [その他のオプション] >[設定] を開き、

<div align="center">
<img src="dataflow_refresh_05.png">
</div> 

[最新の情報に更新] からタイムゾーンとスケジュールを設定することでスケジュール更新が可能です。

<div align="center">
<img src="dataflow_refresh_06.png">
</div> 

データフロー Gen2 CI/CD の場合には、[その他のオプション] > [スケジュール] を選択し、 

<div align="center">
<img src="dataflow_refresh_07.png">
</div> 

表示されたメニューからスケジュールを設定します。
データフロー Gen1 / Gen2 のスケジュール設定は 30 分間隔でしか指定できませんが、CI/CD のスケジュールでは 1 分単位で時間を指定できることや、スケジュール更新を実施する期間を設定できるようになっていることが特長です。

<div align="center">
<img src="dataflow_refresh_08.png">
</div> 

### REST API

以下の REST API を用いることでデータフローを更新することが可能です。

> [!NOTE]
> [Dataflows - Refresh Dataflow - REST API (Power BI Power BI REST APIs) | Microsoft Learn](https://learn.microsoft.com/ja-jp/rest/api/power-bi/dataflows/refresh-dataflow)

必要なパラメータは dataflowId と groupId です。

データフロー Gen1 / Gen2 の場合、これらのパラメータは、 [その他のオプション] > [設定] を開いた際の URL から確認することができます。例えば以下のような URL だった場合には、 /dataflows/ 以降の ”1fbf2a21-363b-4580-baba-b9f9fa54a654” が dataflowId 、 /groups/ 以降の "508a7cbf-c9e8-46f1-8283-908e1fb4293e" が groupId となります。 

> https://app.powerbi.com/groups/508a7cbf-c9e8-46f1-8283-908e1fb4293e/settings/dataflows/1fbf2a21-363b-4580-baba-b9f9fa54a654?language=ja&experience=power-bi

<div align="center">
<img src="dataflow_refresh_09.png">
</div> 

現在のところ、データフロー Gen2 CI/CD ではこの REST API は利用することができません。
代替となる API につきましては現在プレビュー中のため、リリースされることをお待ちください。

> [!NOTE]
> [Fabric Data Factory での Dataflows Gen2 のパブリック API 機能 (プレビュー) - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/data-factory/dataflow-gen2-public-apis)

### Data Factory の Pipeline

ワークスペースを開き、[+新しい項目] から [Data Pipeline] を作成します。

<div align="center">
<img src="dataflow_refresh_10.png">
</div> 

データフロー アクティビティを利用することでデータフロー Gen1 / データフロー Gen2 / データフロー Gen2 CI/CD すべてを更新することが可能です。

<div align="center">
<img src="dataflow_refresh_11.png">
</div> 

リンクされたデータフロー Gen1 以外は自動で更新がされないため、もし連動して更新を実施したい場合には以下のように成功時で連結した構成とします。以下の例では、3つのデータフロー Dataflow Gen1、Dataflow Gen2、Dataflow Gen2 CICD が順に更新が行われ、これらすべての更新が成功した後に Dataflow Gen1 Link Diff の更新が行われます。

<div align="center">
<img src="dataflow_refresh_12.png">
</div> 

データフローを参照しているセマンティック モデルを更新したい場合には、 さらに [セマンティック モデルの更新] アクティビティを追加することもできます。

<div align="center">
<img src="dataflow_refresh_13.png">
</div> 

### Power Automate

Power Automate では [Power Query データフロー アクション] からデータフローの更新を行うことができます。

<div align="center">
<img src="dataflow_refresh_14.png">
</div> 

Power BI のデータフローを更新する場合、[グループの種類] は ”Workspace" を選択します。 "Environment" は Power Apps のデータフローを利用する場合に選択します。残念ながら、現時点ではデータフロー Gen2 CI/CD は Power Automate には対応しておらず、データフローは表示されません。Power Automate から更新を行いたい場合には、データフロー Gen1 または データフロー Gen2 をご利用ください。

<div align="center">
<img src="dataflow_refresh_15.png">
</div> 

## おわりに

今回は データフロー Gen1 / データフロー Gen2 / データフロー Gen2 CI/CD の更新の方法について説明しました。今回取り上げた方法をまとめたのが以下の表です。データフロー以外にご利用いただいているアイテムなども考慮しながら、ご利用いただく更新方法をご検討ください。

|                          | データフロー Gen1 | データフロー Gen2 | データフロー Gen2 CI/CD |
| ------------------------ | :---------------: | :---------------: | :---------------------: |
| オンデマンド更新         |        〇         |        〇         |           〇            |
| スケジュール更新         |        〇         |        〇         |           〇            |
| REST API                 |        〇         |        〇         |       プレビュー        |
| Data Pipeline            |        〇         |        〇         |           〇            |
| Power Automate           |        〇         |        〇         |         未対応          |
| リンクテーブルの連動更新 |        〇         |      未対応       |         未対応          |

以上、本ブログが少しでも皆さまのお役に立てますと幸いでございます。

