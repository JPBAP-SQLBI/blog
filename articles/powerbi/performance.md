---
title: Power BI 利用時のパフォーマンス測定や最適化について
date: 2023-09-30 00:00:00 
tags:
  - Power BI
  - データセット
  - パフォーマンス
--- 

こんにちは、Power BI サポート チームの亀田です。

Power BI Service でデータ更新を行った際に、以下のエラーが発生したことはありませんか。

> Resource Governing: This query uses more memory than the configured limit. The query — or calculations referenced by it — might be too memory-intensive to run. Either simplify the query or its calculations, or if using Power BI Premium, you may reach out to your capacity administrator to see if they can increase the per-query memory limit. More details: consumed memory 6369 MB, memory limit 6144 MB. See https://go.microsoft.com/fwlink/?linkid=2159752 to learn more.

こちらのエラーは、データセットの更新時にクエリあたりのメモリ上限を超過した際に発生するエラーとなります。本エラーが発生した場合、基本的には上位の SKU にアップグレードしてリソースを増強する必要がありますが、データモデルの最適化やビジュアルの修正によってエラーが解消する場合もございます。パフォーマンス改善に役立つ公開情報についてご案内いたします。

<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、　　
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

## 目次

* [Power BI Desktop](#Power-BI-Desktop)
    * [1.データモデルの最適化](#1-データモデルの最適化)
	* [2.パフォーマンスの測定](#2-パフォーマンスの測定)
	* [3.レポート開発･参照の効率化](#3-レポート開発･参照の効率化)
* [Power BI Service](#Power-BI-Service)
* [Power BI Premium Per Capacity (Premium 容量)](#Power-BI-Premium-Per-Capacity-Premium-容量)
* [Microsoft Fabric](#Microsoft-Fabric)

## Power BI Desktop

Power BI Desktop でのパフォーマンス測定･改善については、1) データモデルの改善、 2) パフォーマンスの測定 についてご案内します。

### 1.データモデルの最適化

前提としてデータモデルは、スタースキーマで構築されることが推奨されます。
> [!NOTE]
> 参考# [スター スキーマと Power BI での重要性を理解する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/guidance/star-schema)

処理が複雑となる場合は、 Power BI で列を追加したり、メジャーを作成したりすることや、 Power Query での加工処理を行うと、 Power BI Desktop ではクライアントのリソースを、 Power BI Service では共有リソースを使用するため、データソース側で行うことが望ましいです。 Power BI で変換を行う場合には利用しているデータモデルに応じて以下の公開情報を参照してデータモデルの最適化をご検討ください。
> [!NOTE]
> 参考# [インポート モデリングのデータ削減手法 - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/guidance/import-modeling-data-reduction)
> 参考# [Power BI Desktop の DirectQuery モデルのガイダンス - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/guidance/directquery-model-guidance)
> 参考# [Power BI Desktop の複合モデルのガイダンス - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/guidance/composite-model-guidance)

Power Query を使用する場合には以下のベスト プラクティスをご一読ください。
> [!NOTE]
> 参考# [Power Query を使用するときのベスト プラクティス - Power Query | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-query/best-practices)

### 2.パフォーマンスの測定

パフォーマンス アナライザーを利用することで、レポートでどのビジュアルの表示に時間がかかっているか、またどの部分がボトルネックになっているかを確認することができます。
> [!NOTE]
> 参考# [Power BI Desktop でパフォーマンス アナライザーを使用してレポート要素のパフォーマンスを確認する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/create-reports/desktop-performance-analyzer)

外部ツールとなりますが、 DAX Studio を利用することでもパフォーマンスを確認することができます。DAX Studio を利用する場合には、パフォーマンス アナライザーを利用してクエリ実行時のデータを .json ファイルとしてエクスポートし、エクスポートした .json ファイルを DAX Studio で読み込むことで、クエリの一覧を確認し、実行速度順にクエリを確認することや、また、クエリを再度実行することで DAX Studio 上でクエリの詳細を確認することができます。
> [!NOTE]
> 参考# [Importing Performance Analyzer data into DAX Studio - SQLBI](https://www.sqlbi.com/articles/importing-performance-analyzer-data-in-dax-studio/)

### 3.レポート開発･参照の効率化

レポートの開発時には、 [最適化リボン] を利用することでビジュアルを追加した際のデータ更新を停止することができるため、データソースが大容量の場合であってもデータが読み込まれる時間を削減することができ、効率的な開発が可能です。
> [!NOTE]
> 参考# [Power BI Desktop の最適化リボン - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/create-reports/desktop-optimize-ribbon)
> 参考# [Power BI Desktop の最適化リボンを使用した DirectQuery 最適化のシナリオ - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/create-reports/desktop-optimize-ribbon-scenarios)

また、レポートのスライサーやフィルターが多い場合には、一度にスライサーやフィルターを適用することで、クエリの実行回数を減らすことができます。
> [!NOTE]
> 参考# [レポートにすべてのスライサーを適用およびクリアするボタンを作成する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/create-reports/buttons-apply-all-clear-all-slicers?tabs=powerbi-desktop)
> 参考# [Power BI レポートでフィルターを書式設定する - フィルターの [適用] ボタン | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/create-reports/power-bi-report-filter?tabs=powerbi-desktop#apply-filters-button)

## Power BI Service

現在、プレビュー機能で Power BI Service でもデータモデルの編集が可能ですが、 Power BI Service からデータモデルを編集する場合にも Power BI Desktop で紹介したデータモデルのデータ削減方法が利用できます。
> [!NOTE]
> 参考# [Power BI サービスでデータ モデルを編集する (プレビュー) - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/transform-model/service-edit-data-models)

Power BI Service では、データフローを利用することでデータの加工が可能です。データフローをご利用いただいている場合には以下の公開情報をご一読ください。複数のトピックについてリンクがあります。
> [!NOTE]
> 参考# [データフローのベスト プラクティス - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/transform-model/dataflows/dataflows-best-practices)

<div align="center">
<img src="performance01.png">
</div>  

## Power BI Premium Per Capacity (Premium 容量)

Premium 容量では、パフォーマンスをモニタリングするためのアプリがあります。アプリから時系列で容量の利用率や上限を超過しているかどうかの推移や、各アイテムのリソースの利用状況をご確認いただけます。
> [!NOTE]
> 参考# [Premium メトリック アプリをインストールする - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-premium-install-app?tabs=1st)
> 参考# [Premium メトリック アプリを使用して Power BI Premium 容量を監視します。 - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-premium-metrics-app)
> 参考# [Power BI Premium の最大能力負荷、過負荷、自動スケーリング - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-premium-concepts)
> 参考# [Power BI Premium の CPU スムージング。 - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-premium-smoothing)

また、データセットの使用できるメモリの使用量上限の設定など、データセット、データフローの更新やクエリ、ページ分割されたレポートの実行、AI 機能を処理する各ワークロードの動作を制御することも可能です。
> [!NOTE]
> 参考# [Power BI Premium でワークロードを構成する方法 - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-admin-premium-workloads)

<div align="center">
<img src="performance02.png">
</div>  

Premium 容量の P1･P2 をご利用いただいている場合で、冒頭に記載したクエリあたりの最大メモリエラーが発生している場合、Premium Per User (PPU) 試用版を利用することで、上位の SKU にアップグレードした場合にエラーが解消するかを確認することが可能です。PPU は、 Premium 容量の SKU の P3 に相当するため、試用版を利用して一度更新を実行いただき、エラーが解消する場合には SKU のアップグレードをご検討ください。
> [!NOTE]
> 参考# [Power BI Premium とは - 容量と SKU | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-premium-what-is#capacities-and-skus)
> 参考# [個人として Power BI サービスにサインアップまたは購入する - セルフサービス サインアップを使用して Power BI 有料バージョンの個人向け試用版を開始する | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/fundamentals/service-self-service-signup-for-power-bi#use-self-service-sign-up-to-start-an-individual-trial-of-the-power-bi-paid-version)

<div align="center">
<img src="performance03.png">
</div>  

## Microsoft Fabric

Microsoft Fabric についても、Premium 容量と同様にパフォーマンス測定のためのアプリがあります。Premium 容量と同様に、アプリから時系列で容量の利用率や上限を超過しているかどうかの推移や、各アイテムのリソースの利用状況をご確認いただけます。
> [!NOTE]
> 参考# [Microsoft Fabric Capacity Metrics アプリとは? - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/enterprise/metrics-app)
> 参考# [Microsoft Fabric Capacity Metrics (Microsoft Fabric 容量メトリック) アプリをインストールする - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/enterprise/metrics-app-install?tabs=1st)
> 参考# [メトリック アプリの概要ページを理解する - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/enterprise/metrics-app-overview-page)
> 参考# [メトリック アプリのタイムポイント ページについて - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/enterprise/metrics-app-timepoint-page)

以上、本ブログが少しでも皆さまのお役に立てますと幸いでございます。
