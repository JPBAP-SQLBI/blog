---
title: Microsoft Fabric の OneLake について
date: 2024-06-28 15:00:00 
tags:
  - Microsoft Fabric
  - OneLake
  - ショートカット
---


こんにちは、Power BI サポート チーム チャンです。

Microsoft Fabric (以下 Fabric) 環境では、OneLake という組織全体で 1 つに統合された論理データ レイクがあります。データ ウェアハウスやレイクハウスなどのファブリック データ項目はすべて、データを Delta Parquet 形式で OneLake に自動的に格納します。この記事では、OneLake の利用条件や概要、その他 OneLake にまつわるよくある質問とその関連の説明をご案内します。

<!-- more -->


> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
## 目次
---
 - [ライセンス要件](#ライセンス要件)
 - [概要](#概要)
 - [よくある質問](#よくある質問)

---
## ライセンス要件
---
OneLake をご利用いただくには、以下のいずれかのライセンスをご契約いただく必要があります。

- Fabric 容量 (F SKU) 
- Premium 容量 (P SKU) 
- Fabric 試用版※

※ Fabric 試用版は 60 日間有効で、Fabric 容量 (F SKU) の F64 と同等のものをご利用いただけますが、試用版のため一部の機能（ Copilot 、信頼されたワークスペース アクセス、およびマネージド プライベート エンドポイント）は使用できません。また、OneLake ストレージを最大 1 TB まで取得できます。

有償ライセンス及び試用版の詳細については以下の公開情報をご参照ください。

> [!NOTE]
> 有償ライセンス - 参考# [Microsoft Fabric ライセンス](https://learn.microsoft.com/ja-jp/fabric/enterprise/licenses)
> 試用版 - 参考# [Microsoft Fabric 試用版の容量](https://learn.microsoft.com/ja-jp/fabric/get-started/fabric-trial)

---
## 概要
---
OneLake は、組織全体の単一の統合された論理データ レイクであり、すべての Fabric テナントに対して自動的にプロビジョニングされます。 また、データ ウェアハウスやレイクハウスなどのすべての Fabric アイテムは、データを OneLake に自動的に保存します。

また、ショートカットを作成することで、OneLake の外部にあるデータを移動・複製せずともそのまま利用できます。例えば Azure Data Lake Storage Gen2 (ADLS Gen2) 、 Amazon S3 、 Dataverse 、 Google Cloud Storage にあるデータに対して、ショートカットを作成してそのままアクセスできます。


<div align="left">
<img src="https://learn.microsoft.com/ja-jp/fabric/onelake/media/onelake-overview/fabric-shortcuts-structure-onelake.png">
</div>
</p>

> [!NOTE]
> 参考# [OneLake のショートカット](https://learn.microsoft.com/ja-jp/fabric/onelake/onelake-shortcuts)

---
## よくある質問
---
OneLake にまつわるよくある質問とその関連の説明をご案内します。

#### 質問１： OneLake に格納されたデータは別途課金されますか。
Microsoft Fabric のリソースを購入いただく場合、 Fabric 容量 (F SKU) によって自動的にプロビジョニングされる OneLake に格納されるデータは、使用したストレージ容量に応じて請求されます。

料金の詳細につきましては、以下の公開情報をご確認ください。

> [!NOTE]
> 参考# [Microsoft Fabric の価格](https://azure.microsoft.com/ja-jp/pricing/details/microsoft-fabric/)

一方で、Fabric 試用版は、OneLake にデータを格納しても課金されません。
Premium 容量 (P SKU) をご利用いただく場合、現時点（執筆の 2024 年 6 月末時点）では OneLake のデータストレージに応じて請求を行っていません。

しかしながら、Premium 容量 (P SKU) は 2024 年 7 月より新規契約できなくなり、すでに Premium 容量をご契約中のお客様は、現在の契約更新日が 2025 年 1 月 1 日以降となっている場合には、 Fabric 容量 (F SKU) へ移行する必要があります。

詳細につきましては、以下のブログ記事をご確認ください。

> [!NOTE]
> 参考# [Important update coming to Power BI Premium licensing](https://powerbi.microsoft.com/en-us/blog/important-update-coming-to-power-bi-premium-licensing/)

---

#### 質問２： Power BI のレポートやセマンティックモデルは、 OneLake にありますか。
Power BI のレポートやセマンティックモデルは OneLake にありません。

OneLake に格納され、Fabric 容量 (F SKU) に紐付けられて請求されるものは、Fabric Capacity Metrics アプリの [Storage] (ストレージ) ページにて確認できます。

現時点（執筆の 2024 年 6 月末時点）で OneLake にデータが格納され、ストレージ容量の請求に関わる項目は、以下でございます。

- Reflex
- レイクハウス
- Eventstream / KQL データベース / KQL クエリセット

最新の詳細情報につきまして、以下の公開情報をご確認ください。
> [!NOTE]
> 参考# [メトリック アプリのストレージ ページについて](https://learn.microsoft.com/ja-jp/fabric/enterprise/metrics-app-storage-page)

---

#### 質問３： OneLake データ ハブで表示される項目はすべて OneLake にありますか。

OneLake データハブに表示されるのは、アクセス権のある組織内の Fabric (Power BI を含めて) データ項目となっていますので、実際 OneLake に格納されていないレポートやセマンティックモデルも含まれます。OneLake に格納されている項目を確認するには、Fabric Capacity Metrics アプリの [Storage] (ストレージ) ページにて確認することができます。


OneLake データハブの仕様につきまして、以下の公開情報をご確認ください。
> [!NOTE]
> 参考# [OneLake データ ハブでデータ項目を検出する](https://learn.microsoft.com/ja-jp/fabric/get-started/onelake-data-hub)

---

#### 質問４： Windows 用 OneLake ファイル エクスプローラーはどのようなファイル形式がサポートされていますか。
Windows 用 OneLake ファイル エクスプローラーは、現時点ではプレビュー機能であり、今後予告なく機能が変更される、または削除される可能性があるため、本番環境での利用はお控えください。

また、基本的にレイクハウスやウェアハウスの Fabric 項目のメタデータの同期が実行されますので、現時点では、明示的にサポートされているファイル拡張子の情報がございません。

以下の公開情報より、1.0.11.0 以降のバージョンでは、csv ファイルまたは Excel のアップロード及び更新はサポートされます。

> [!NOTE]
> 参考# [Excel を使用してファイルを更新する機能 - 最新の OneLake エクスプローラーの新機能](https://learn.microsoft.com/ja-jp/fabric/onelake/onelake-file-explorer-release-notes#ability-to-update-files-using-excel)


[Files] 配下にアップロードすると、ワークスペース上のレイクハウスの [Files] 配下に反映されます。

<div align="left">
▼ ローカルに同期されたレイクハウスアイテムの Files 配下に Excel ファイルを配置します。
</br>
<img src="2.png">
</br>

▼ 同レイクハウスアイテムをサービス上で、 Files 配下に反映されることを確認します。
<img src="1.png">
</br>
</div>


---

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)