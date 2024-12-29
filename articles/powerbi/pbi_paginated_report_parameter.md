---
title: ページ分割されたレポート② パラメーターを利用したレポート
date: 2024-11-30 00:00:00 
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
# ページ分割されたレポート②

こんにちは、Power BI サポート チームの亀田です。

Power BI では、.pbix ファイルとして Power BI Desktop で作成できるレポートのほかに、.rdl ファイルとして作成できるページ分割されたレポートを作成することができます。ページ分割されたレポートは、請求書や帳票などの、多くの行項目を含むレポートを作成するのに便利です。

過去には [ページ分割されたレポート①](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_paginated_report_1/) で簡単なレポートの作成について説明しました。今回は、パラメーターを利用したレポートを作成する方法について説明します。

<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、　　
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

## 目次

* [パラメーターとは](#パラメーターとは)
* [パラメーターの作成](#パラメーターの作成)
    * [データソースの作成](#データ-ソースの作成)
    * [データセットの作成](#データセットの作成)
    * [パラメーターの作成](#パラメーターの作成-1)
    * [パラメーターで絞り込みを行うデータセットの作成](#パラメーターで絞り込みを行うデータセットの作成)
    * [レポートの作成](#レポートの作成)
    * [レポートの実行](#レポートの実行)
* [おわりに](#おわりに)

## パラメーターとは

パラメーターは、Power BI のページ分割されたレポートで使用される機能で、レポートの動的なカスタマイズを可能にします。ユーザーがレポートを実行する際に、特定の条件や値を指定することで、取得するデータや表示内容を制御できるようになります。

ユーザーが必要なデータを特定し、簡単にフィルタリングできるため、データセット全体を出力する必要がなくなります。また、必要なデータだけを取得するクエリにより、サーバーの負荷を軽減し、処理時間を短縮することができます。

<div align="center">
<img src="paginated_report_parameter_00.png">
</div>

## パラメーターの作成

それでは、パラメーターを作成してみましょう。データソースには [AdventureWorks サンプル データベース - SQL Server | Microsoft Learn](https://learn.microsoft.com/ja-jp/sql/samples/adventureworks-install-configure?view=sql-server-ver16&tabs=ssms) を使用します。

今回例として作成するパラメーターは、 "ProductCategory" と "Product" の2つです。 "ProductCategory" を選択すると、そのカテゴリに所属する選択可能な "Product" が表示されるので、選択してレポートを表示します。このような依存関係があるパラメーターはカスケード型パラメーターと呼ばれます。

> [!NOTE]
> 参考# [ページ分割されたレポートでカスケード型パラメーターを使用する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/guidance/paginated-report-cascading-parameter#filter-by-related-columns)

### データ ソースの作成

初めに、データ ソースを追加します。 [データ ソース] を右クリック > [データ ソースの追加] を選択します。
<div align="center">
<img src="paginated_report_parameter_01.png">
</div>

[ビルド] を選択し、接続先を入力して [OK] を選択します。
<div align="center">
<img src="paginated_report_parameter_02.png">
</div>

### データセットの作成

パラメーターに利用するデータセットを作成します。今回は "ProductCategory" と "Product" の2つのパラメーターを作成します。

[データセット] を右クリック > [データセットの追加] を選択します。

<div align="center">
<img src="paginated_report_parameter_03.png">
</div>

データ ソースを選択し、 [クエリ デザイナー] を選択します。

<div align="center">
<img src="paginated_report_parameter_04.png">
</div>

パラメーターで利用するデータの含まれるテーブルを選択し、 [OK] を選択します。

<div align="center">
<img src="paginated_report_parameter_05.png">
</div>

クエリが作成されたことを確認して、 [OK] を選択します。

<div align="center">
<img src="paginated_report_parameter_06.png">
</div>

同様に、 パラメーター "Product" も作成します。

<div align="center">
<img src="paginated_report_parameter_07.png">
</div>

### パラメーターの作成

データセットが作成できたら、パラメーターを作成します。はじめに、パラメーター "ProductCategory" を作成します。 

[パラメーター] を右クリック > [パラメーターの追加] を選択します。

<div align="center">
<img src="paginated_report_parameter_08.png">
</div>

[名前] 、 [プロンプト] を入力します。 [プロンプト] はパラメーターの横に表示されるテキストです。

<div align="center">
<img src="paginated_report_parameter_09.png">
</div>

<div align="center">
<img src="paginated_report_parameter_10.png">
</div>

[使用できる値] で [クエリから値を取得] を選択し、[データセット] には先程作成したデータセットを指定します。 [値フィールド] には、絞り込みに利用するカラムを指定します。パラメーターを利用したデータセットの絞り込みを行う際に WHERE 句に利用されます。 [ラベル フィールド] には、ユーザーがパラメーターの選択時に表示させたいカラムを指定します。

<div align="center">
<img src="paginated_report_parameter_11.png">
</div>

[固定値] 、 [詳細設定] は今回変更せず、 [OK] を選択します。

次に、パラメーター "Product" を作成しますが、その前に先ほど作成したデータセット "Product" を編集します。

[Product] を右クリック > [データセットのプロパティ] を選択します。

<div align="center">
<img src="paginated_report_parameter_12.png">
</div>

クエリの最後に WHERE 句を追加します。パラメーターを指定する場合には、 "@<パラメーター名>" で指定を行います。これで、パラメーター "ProductCategory" を選択することでデータ ソース "Product" が絞り込まれることになります。追加したら、 [OK] を選択します。

> WHERE
>   Product.ProductCategoryID = @ProductCategory

<div align="center">
<img src="paginated_report_parameter_13.png">
</div>

[パラメーター] を右クリック > [パラメーターの追加] を選択し、 パラメーター "Product" を作成します。

<div align="center">
<img src="paginated_report_parameter_14.png">
</div>

[使用できる値] には データセット "Product" を指定します。[既定値] 、 [詳細設定] は変更せず、 [OK] を選択します。

<div align="center">
<img src="paginated_report_parameter_15.png">
</div>

これで、パラメーターが作成できました。あとは、パラメーターでフィルターを行うトランザクション データを作成し、レポートを作成していきます。

## パラメーターで絞り込みを行うデータセットの作成

これまで作成したパラメーターを利用して絞り込みを行うデータセットを作成していきます。

[データセット] を右クリック > [データセットの追加] を選択します。 [クエリ デザイナー] を選択します。

<div align="center">
<img src="paginated_report_parameter_16.png">
</div>

パラメーターを作成した "Product" 、 "ProductCategory" テーブルと、トランザクション データを含むテーブル "SalesOrderDetail" を選択し [OK] を選択します。

<div align="center">
<img src="paginated_report_parameter_17.png">
</div>

クエリが追加されたことを確認し、 WHERE 句を追加します。[OK] を選択します。

> WHERE
>   Product.ProductCategoryID = @ProductCategory
>   AND Product.ProductID = @Product

<div align="center">
<img src="paginated_report_parameter_18.png">
</div>

これで、パラメーターを作成して絞り込みを行うためのデータセットが作成できました。

## レポートの作成

それでは、これまで作成したデータを利用してテーブルを作成します。

[挿入] タブ > [テーブル] > [テーブル ウィザード] を選択します。

<div align="center">
<img src="paginated_report_parameter_19.png">
</div>

データセット "SalesOrderDetail" を選択して [次へ] を選択します。

<div align="center">
<img src="paginated_report_parameter_20.png">
</div>

テーブルを作成します。例として [行グループ] に "ProductCategory_Name" 、 "Product_Name" 、 [値] に "UnitPrice" 、 "UnitPriceDiscount" 、 "OrderQty"  を指定します。 Sum 関数は項目を選択すると自動で付与されます。

<div align="center">
<img src="paginated_report_parameter_21.png">
</div>

"小計と総計を表示" "グループの展開/折りたたみ" を設定し、 [次へ] を選択します。

<div align="center">
<img src="paginated_report_parameter_22.png">
</div>

プレビューが表示されるので、問題なければ [完了] を選択します。

<div align="center">
<img src="paginated_report_parameter_23.png">
</div>

## レポートの実行

[ホーム] タブ > [実行] から作成したレポートを実行します。

<div align="center">
<img src="paginated_report_parameter_24.png">
</div>

正しく設定ができていれば、 "ProductCategory" を選択することで "Product" が選択できるようになります。

<div align="center">
<img src="paginated_report_parameter_25.png">
</div>

どちらも選択した状態で [レポートの表示] を選択することでレポートが表示されます。

<div align="center">
<img src="paginated_report_parameter_26.png">
</div>

## おわりに

パラメーターを含むより詳細なレポートの作成方法について説明しました。パラメーターを利用することで、よりユーザーが利用しやすいレポートが作成できます。公開情報には、今回作成したパラメーターの他にも、グルーピングを行う方法なども紹介されておりますので、お試しいただけますと幸いです。

> [!NOTE]
> 参考# [ページ分割されたレポートでカスケード型パラメーターを使用する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/guidance/paginated-report-cascading-parameter)

以上、本ブログが少しでも皆さまのお役に立てますと幸いでございます。