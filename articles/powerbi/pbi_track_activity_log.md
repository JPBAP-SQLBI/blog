---
title: ユーザーの操作におけるPower BIのアクティビティログ
date: 2024-02-29 00:00:00 
tags:
  - Power BI
  - activity-log

---


こんにちは、Power BI サポート チームのファムです。

Power BI のアクティビティログは、Power BIサービスにおけるユーザーの操作がログとして記録されています。アクティビティログから、特定のユーザーが実行した操作、時間、データの変更、共有、エクスポートなどの詳細な情報を確認することができます。Power BI のユーザーアクティビティ追跡方法について、[こちらのブログ](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_activity_log_usage_metrics/)をご参考ください。

本ブログでは、ユーザーのどの操作でどのログが記録されるか、よく利用される操作のアクティビティログについてご紹介いたします。

<!-- more -->

</br>

> [!IMPORTANT]
> 弊社サポートをご利用いただいている場合、状況に合わせた調査方針を策定するため、記載の内容とご案内が異なる場合がございます。
> ご不明な点がございましたら弊社サポート担当までお気軽にご質問ください。
> また掲載している画像・手順は投稿時点のものとなります。最新の情報とは異なる可能性がございますので予めご了承ください。

</br>

---
## 目次
---
1. [アクティビティログの確認](#1．アクティビティログの確認)
2. [アクティビティログの操作の詳細](#2．アクティビティログの操作の詳細)

</br>

---

## 1．アクティビティログの確認
PowerShell を使ってユーザーアクティビティのログを出力できる機能がございます。詳細な手順については、[こちらのブログ](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_activity_log_usage_metrics/)の［ActivityEvents］の項目をご確認ください。その手順で、誰（UserID）、いつ（CreationTime）、操作（Operation）、レポート名（ReportName）、ワークスペース名（WorkSpaceName）などの情報が追跡できます。

以下画面の実行例では、admin＠M365x86598379.onmicrosoft.comが、2024-02-21T15:46:32Zに ”アクティビティログ検証（directquery）”というレポートをエクスポートしたことが確認できます。


</br>

<div align="center">
<img src="pic1.png">
</div>


## 2．アクティビティログの操作の詳細

> **アクティビティログの操作一覧の参考情報**
>  [操作一覧](https://learn.microsoft.com/ja-jp/fabric/admin/operation-list)


例として、以下のアクティビティログが、実際にどのような操作かについてご紹介いたします。
・DownloadReport
・ExportActivityEvents
・ExportReport
・ExportDataflow
・ExportTile

**■アクティビティログ：DownloadReport**
概要：Power BI レポートのダウンロード
操作：「ファイル」 ＞ 「このファイルをダウンロードする」をクリックする操作 

</br>

<div align="center">
<img src="pic2.png">
</div>


**■アクティビティログ：ExportActivityEvents**
概要：Power BI アクティビティ イベントのエクスポート
操作：「ExportActivityEvents」のアクティビティログは、以下の４つの操作でご確認いただけます。

1．レポートの「エクスポート」 ＞ 「Excelで分析」をクリックする操作
※アクティビティログのAnalyzeInExcelも表示されます。

</br>

<div align="center">
<img src="pic3.png">
</div>


2．レポートの「エクスポート」 ＞ 「PowerPoint」 ＞ 「画像を埋め込む」をクリックする操作
※アクティビティログのExportArtifactも表示されます。

</br>

<div align="center">
<img src="pic4.png">
</div>


3．レポートの「エクスポート」 ＞ 「PowerPoint」 ＞ 「ライブ データを埋め込む」をクリックする操作
※アクティビティログのGetSnapshotsも表示されます。

</br>

<div align="center">
<img src="pic5.png">
</div>


4．レポートの「エクスポート」 ＞ 「PDF」をクリックする操作
</br>

<div align="center">
<img src="pic6.png">
</div>

**■アクティビティログ：ExportReport**
概要：Power BI レポートを別のファイル形式またはエクスポートされたレポート ビジュアル データにエクスポートしました
操作：レポートの三点リーダーから、「データのエクスポート」 ＞ 「エクスポート」をクリックする操作

</br>

<div align="center">
<img src="pic7.png">
</div>


**■アクティビティログ：ExportDataflow**
概要：Power BI データフローをエクスポートしました
操作：データフローの三点リーダーから、「.jsonのエクスポート」をクリックする操作

</br>

<div align="center">
<img src="pic8.png">
</div>


**■アクティビティログ：ExportTile**
概要：Power BI タイル データをエクスポートしました
操作：ダッシュ―ボードのビジュアルの三点リーダーから、「CSVにエクスポートする」をクリックする操作

</br>

<div align="center">
<img src="pic9.png">
</div>

</br>


以上、本ブログ が少しでも皆様のお役に立てますと幸いでございます。


---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)
