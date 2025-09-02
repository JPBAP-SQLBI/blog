---
title: Cognitive service と Azure ML の廃止
date: 2025-08-31 00:00:00 
tags:
  - Power BI
  - Power BI Desktop
  - Power BI サービス
  - Premium
  - AI
  - アナウンス
---

こんにちは、Power BI サポート チームの亀田です。

[Cognitive services and Azure ML will be fully retired by September 15th, 2025 | Microsoft Power BI Blog | Microsoft Power BI](https://powerbi.microsoft.com/en-us/blog/cognitive-services-and-azure-ml-for-dataflows-will-be-fully-retired-by-september-15th-2025/) でアナウンスがされておりますとおり、Power BI の Premium 機能として提供されていた Cognitive service と Azure ML を利用する AI 機能が 2025 年 9 月 15 日以降利用できなくなります。機能の廃止に伴い、 2025 年 8 月 11 日よりこれらの AI 機能を利用した セマンティック モデルを新しく作成することはできません。今回はこれらの機能を利用しているユーザーが必要な対応についてご案内いたします。

<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、　　
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

## AI 機能の廃止について

冒頭でご案内しました Power BI Blog [Cognitive services and Azure ML will be fully retired by September 15th, 2025 | Microsoft Power BI Blog | Microsoft Power BI](https://powerbi.microsoft.com/en-us/blog/cognitive-services-and-azure-ml-for-dataflows-will-be-fully-retired-by-september-15th-2025/) で今回廃止の対象となった Cognitive service と Azure ML は Power BI Premium 容量や Power BI Premium Per User のライセンス保有ユーザーが利用できた Premium 機能の一つです。Power Query 内でユーザーが用意したデータを利用してキー フレーズ抽出や感情分析などを行うことができました。本変更は、拡張性や柔軟性向上を求めるユーザーからのフィードバックに基づき決定されました。

## 影響を受ける機能

影響を受ける機能は Cognitive service  および Azure ML です。

- Cognitive Services 
  - 感情分析
  - キーフレーズ抽出
  - 言語検出 
  - 画像タグ付け

- Azure ML 
  - Power Query から Azure ML モデルへのアクセス

## スケジュール

**2025年8月11日**: 新規モデルの作成停止
- Cognitive Servicesを使用した新しいモデルの作成ができなくなります。
  利用しようとした場合にはエラーが発生します。
  <div align="center">
  <img src="Retirement-CognitiveServices-and-AzureML_03.png">
  </div>  
- 既存モデルの更新は 9 月 15 日 まで引き続き可能です。

**2025年9月15日**: 完全廃止
- Cognitive ServicesとAzure MLを使用するすべての機能が利用不可になり、既存モデルの更新が失敗するようになります。

 ## 必要な対応

セマンティック モデル内で Cognitive service  および Azure ML を利用している場合には 9 月 15 日以降セマンティック モデルの更新が失敗するようになりますので、セマンティック モデル内のクエリから利用しているステップを削除する必要があります。削除手順は以下の通りです。

1. セマンティック モデルを Power BI Service からダウンロードし、Power BI Desktop で [データの変換] を選択し Power Query を開きます。
  <div align="center">
  <img src="Retirement-CognitiveServices-and-AzureML_01.png">
  </div> 
2. [適用したステップ] から Cognitive service  および Azure ML を利用しているステップを削除します。
  <div align="center">
  <img src="Retirement-CognitiveServices-and-AzureML_02.png">
  </div> 

データフローを利用している場合など、 Power BI Service 内で利用できる Power Query Online の場合でも同様の手順で Cognitive service  および Azure ML を含むステップを削除します。 

引き続き AI 機能を利用したい場合には、現時点でプレビュー機能ではございますが、 Microsoft Fabric で利用できる AI 機能がございますので、こちらのご利用をご検討ください。
参考# [Fabric の Azure AI サービスを使用する - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/data-science/ai-services/ai-services-overview)
参考# [Fabric の AutoML の概念 (プレビュー) - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/data-science/automated-machine-learning-fabric)

## おわりに

今回は Cognitive service と Azure ML の廃止についてご案内いたしました。2019 年 6 月 10 日に本機能が GA されてからおおよそ 6 年間、ご利用いただいた皆さまには感謝申し上げます。引き続き Microsoft Fabric の AI 機能をご利用いただけますと幸いです。

以上、本ブログが少しでも皆さまのお役に立てますと幸いでございます。