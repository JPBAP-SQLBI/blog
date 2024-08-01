---
title: ページ分割されたレポート①
date: 2024-07-31 00:00:00 
tags:
  - Power BI
  - Power BI サービス 
  - Power BI レポート ビルダー
  - 改ページ対応レポート
  - ページ分割されたレポート 
  - Paginated reports
  - Power BI Report Builder 
  - SQL Server Reporting Services
  - SSRS
  - Power BI Report Server
  - PBIRS
  - Creator
---
# ページ分割されたレポート①

こんにちは、Power BI サポート チームの亀田です。

Power BI では、.pbix ファイルとして Power BI Desktop で作成できるレポートのほかに、.rdl ファイルとして作成できるページ分割されたレポートを作成することができます。ページ分割されたレポートは、請求書や帳票などの、多くの行項目を含むレポートを作成するのに便利です。今回は、ページ分割されたレポートと、レポートを作成するための Power BI Report Builder について説明します。

<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、　　
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

## 目次

* [ページ分割されたレポートとは](#ページ分割されたレポートとは)
* [Power BI Report Builder でのレポート作成](#Power-BI-Report-Builder-でのレポート作成)
    * [準備 : Power BI Report Builder のインストール](#準備-Power-BI-Report-Builder-のインストール)
    * [新規レポートの作成と発行](#新規レポートの作成と発行)
* [おわりに](#おわりに)

## ページ分割されたレポートとは

ページ分割されたレポートは、1ページに収まるように設定されているレポートで、印刷や共有することを想定してデザインされたレポートです。従来よりオンプレミス製品である SQL Server Reporting Services (SSRS) では、ページ分割されたレポートを作成することができましたが、 Power BI でも同様に作成することができます。ページ分割されたレポートは SSRS と Power BI のどちらで作成した場合でも RDL (Report Definition Language) で定義されていますが、SSRS の場合には Microsoft Report Builder を利用するのに対し、Power BI の場合には Power BI Report Builder を利用しますのでインストール時にはご注意ください。

> [!NOTE]
> [Power BI のページ分割されたレポートとは - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/paginated-reports/paginated-reports-report-builder-power-bi)
> [Power BI サービスでのページ分割されたレポート - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/consumer/end-user-paginated-report)
> [レポート定義言語 (SSRS) - SQL Server Reporting Services (SSRS) | Microsoft Learn](https://learn.microsoft.com/ja-jp/sql/reporting-services/reports/report-definition-language-ssrs?view=sql-server-ver16)

作成されたレポート請求書や帳票などの、多くの行項目を含むレポートを作成したい場合、ページ分割されたレポートが適切です。例えば、通常のレポートを印刷しようとした場合、 Power BI Service では以下のように表示されます。

<div align="center">
<img src="paginated1-01.png">
</div>

このレポートを印刷しようとすると、以下のとおり現在見えているデータのみが印刷対象となります。

<div align="center">
<img src="paginated1-02.png">
</div>

一方、ページ分割されたレポートの場合には、 Power BI Service 上では以下のように表示されます。

<div align="center">
<img src="paginated1-03.png">
</div>

そして、印刷しようとすると、すべてのデータが印刷対象となります。

<div align="center">
<img src="paginated1-04.png">
</div>

このように、ページ分割されたレポートは多くの行項目を一度に出力したい場合に向いているレポートです。

そして、ページ分割されたレポートから出力した場合、データ行に上限はありません。(しかしながら、大量データをエクスポートした場合には高負荷となることが想定されますので、御理解の上ご利用ください。)

また、ページ分割されたレポートでは、ユーザーにパラメーターを入力させ、入力されたパラメーターをもとにレポートを生成することが可能です。そうすることで、例えば売上データの開始日と終了日を指定したり、特定の製品のみを対象としたレポートを出力することが可能となります。

> [!NOTE]
> [Power BI サービスでページ分割されたレポートのパラメーターを作成する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/paginated-reports/parameters/paginated-reports-create-parameters)
> [Power BI レポート ビルダーでのレポート パラメーター - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/paginated-reports/parameters/report-builder-parameters)

## Power BI Report Builder でのレポート作成

今回は、シンプルなレポートの作成方法と発行方法を説明します。

### 準備 : Power BI Report Builder のインストール

Power BI Report Builder を以下のリンクからダウンロードし、インストールしておきます。

> [!NOTE]
> [Download Microsoft® Power BI Report Builder from Official Microsoft Download Center](https://www.microsoft.com/ja-jp/download/details.aspx?id=105942)

また、今回のレポートには AdventureWorks のサンプル データベースを使用しています。

> [!NOTE]
> [AdventureWorks サンプル データベース - SQL Server | Microsoft Learn](https://learn.microsoft.com/ja-jp/sql/samples/adventureworks-install-configure?view=sql-server-ver16&tabs=tsql)

### 新規レポートの作成と発行

1. はじめに、 [ホーム] > [新規作成] を選択します。
    <div align="center">
    <img src="paginated1-05.png">
    </div>

2.  [新しいレポート] > [テーブルまたはマトリックス ウィザード] を選択します。
    <div align="center">
    <img src="paginated1-06.png">
    </div>

3.  [データセットの選択] が表示されるので、 [データセットを作成する] を選択し、 [次へ] を選択します。
    <div align="center">
    <img src="paginated1-07.png">
    </div>

4.  [データソースへの接続の選択] が表示されるので、 [新規] を選択します。
    <div align="center">
    <img src="paginated1-08.png">
    </div>

5.  [データソースのプロパティ] ウインドウが表示されるので、 [ビルド] を選択して接続先を設定します。設定したら [OK] を選択します。
    <div align="center">
    <img src="paginated1-09.png">
    </div>

6.  [データソースへの接続の選択] 画面に戻るので、先ほど作成したデータソースを選択し、 [次へ] を選択します。資格情報の入力が求められたら、入力して [OK] で進みます。
    <div align="center">
    <img src="paginated1-10.png">
    </div>

7.  データソースが表示されるので、レポートで使用したいデータを選択します。 [次へ] を選択します。
    <div align="center">
    <img src="paginated1-11.png">
    </div>

8.  [フィールドの配置] ウインドウが表示されるので、テーブル / マトリックスで使用したいデータを指定します。 [値] については自動的に SUM で集計されます。 [次へ] を選択します。
    <div align="center">
    <img src="paginated1-12.png">
    </div>

9. レイアウトのプレビューが表示されます。プレビューでは一行しか表示されませんが、実際にレポートを表示した際にはデータが表示されますのでご安心ください。
    <div align="center">
    <img src="paginated1-13.png">
    </div>

10. デザイン画面が表示されます。
    <div align="center">
    <img src="paginated1-14.png">
    </div>

11.  [実行] すると、先ほどのレイアウトのレポートが実際のデータで表示されます。
    <div align="center">
    <img src="paginated1-15.png">
    </div>

12. 実際に表示されるレポート例です。
    <div align="center">
    <img src="paginated1-16.png">
    </div>

13. グラフを追加したい場合には、 [挿入] タブから [グラフ] を選択します。
    <div align="center">
    <img src="paginated1-17.png">
    </div>

14. 追加したいグラフを選択します。
    <div align="center">
    <img src="paginated1-18.png">
    </div>

15. グラフを右クリックして、グラフで使用するデータを指定します。
    <div align="center">
    <img src="paginated1-19.png">
    </div>

16. 再度 [実行] してみると、グラフが表示されていることを確認できます。
    <div align="center">
    <img src="paginated1-20.png">
    </div>

17. レポートを発行する場合には、 [ファイル] > [公開] > [Power BI サービス] を選択します。サインインをしていない場合にはサインインのポップアップが表示されますので、サインインを行います。
    <div align="center">
    <img src="paginated1-21.png">
    </div>

18. 発行先を選択し、ファイル名を入力して [公開] を選択します。
    <div align="center">
    <img src="paginated1-22.png">
    </div>
    
19. 正常に発行が行われれば、選択したワークスペースにページ分割されたレポートとして発行されます。
    <div align="center">
    <img src="paginated1-23.png">
    </div>

## おわりに

今回はページ分割されたレポートについてご説明いたしました。次回はパラメーターを含むより詳細なレポートの作成方法についてご説明いたします。

以上、本ブログが少しでも皆さまのお役に立てますと幸いでございます。
