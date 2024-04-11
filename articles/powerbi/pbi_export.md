---
title: エクスポート可能なファイルの種類について
date: 2022-06-30 00:00:00 
tags:
  - Power BI　　
  - Power BI サービス
  - エクスポート
  - Admin
  - Consumer
---

こんにちは、Power BI サポート チームの山崎です。

Power BI 管理者様や IT 部門のご担当者様から、「レポートのデータが外に持ち出されないか心配」というご相談をいただくことがあります。
Power BI サービス上での外部への情報漏洩という観点では、以下 Blog をご参考にしていただければと思いますが、今回は Power BI サービス上でファイルとして出力する機能の制御についてご案内いたします。  

<!-- more -->


Power BI サービスでは、レポートを PBIX ファイルだけでなく一部データを CSV ファイルや XLSX ファイルなどにエクスポートすることができますので、組織内のセキュリティポリシーや運用にあった設定をご検討いただければと思います。


> **ご参考情報：**
> [組織外のユーザーとPower BIコンテンツの共有](https://jpbap-sqlbi.github.io/blog/powerbi/aad_guestuser/)
> [Power BI レポートの埋め込み方法の種類について - ３．Webに公開（パブリック）](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_embed/)

</br>

> [!IMPORTANT]
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、
> 本記事編集時点と実際の機能に相違がある場合がございます。
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---

### エクスポート可能なファイルの種類について

現在 Power BI サービスでは、コンテンツのデータを以下ファイルへエクスポートすることがサポートされており、これらの機能は管理ポータルにて、組織全体またはグループ単位で許可するかどうか制御が可能です。
ファイルの種類によって制限事項などがありますので、それぞれ公開情報をご参考にしていただきますようお願いいたします。

・XLSX ファイル
・CSV ファイル
・PBIX ファイル
・PPTX ファイル
・PDF ファイル
・MHTML ファイル（ページ分割されたレポートのみ）
・DOCX ファイル（ページ分割されたレポートのみ）
・XML ファイル（ページ分割されたレポートのみ）
・PNG ファイル
・印刷

#### 設定項目
“管理ポータル > テナント設定 > エクスポートと共有の設定” 配下にある以下項目にて、組織全体 または グループ単位で許可するかどうか設定します。
黄色枠で囲っている項目は、ページ分割されたレポートが対象となる項目です。

ご参考情報:
[エクスポートと共有の管理者設定](https://learn.microsoft.com/ja-jp/power-bi/admin/service-admin-portal-export-sharing)

<div align="center">
<img src="1.png">
</div>


##### レポートで表示されるエクスポート項目

<div align="center">
<img src="1-1.png">
</div>

##### ページ分割されたレポートで表示されるエクスポート項目

<div align="center">
<img src="1-2.png">
</div>

---
### 各設定の公開情報と概要


#### XLSX ファイル 、CSV ファイル
ビジュアルの作成に使用されているデータをエクスポートします。
そのビジュアルで表示されている内容のデータ（概要データ）を XLSX ファイルまたは CSV ファイルへ、基データを XLSX ファイルへエクスポートできます。
概要データについては、XLSX ファイルのほうが CSV ファイルより多くの行数をエクスポートできます。
また、マトリックスやテーブルビジュアルの場合は、現在のレイアウトのデータを XLSX ファイルにエクスポートすることもできます。
なお、テナント設定以前に、Power BI Desktop のオプション設定やレポート設定画面にて、レポート毎にエクスポートを許可するかどうかを設定することも可能です。


必要な権限：
概要データと現在のレイアウトのデータのエクスポートは、閲覧権限を持っているユーザーにて操作可能です。
基データのエクスポートは、ワークスペースに対して共同作成者以上のロールが割り当てられているユーザーにて操作可能です。

ご参考情報:：
[視覚エフェクトの作成に使用されたデータをエクスポートする](https://learn.microsoft.com/ja-jp/power-bi/visuals/power-bi-visualization-export-data?tabs=dashboard)


<div align="center">
<img src="2-1.png">
</div> 

▼ マトリックスやテーブルビジュアルの場合は、現在のレイアウトのデータがエクスポート可能
<div align="center">
<img src="2-2.png">
</div> 

#### PBIX ファイル
Power BI Desktop で作成した後に発行またはアップロードされたレポートに限り、レポートまたはデータセットから PBIX ファイルとしてエクスポートできます。


必要な権限：
レポートが存在するワークスペースの共同作成者にて操作可能です。

ご参考情報：
[Power BI サービスから Power BI Desktop にレポートをダウンロードする](https://learn.microsoft.com/ja-jp/power-bi/create-reports/service-export-to-pbix)


▼ レポートからエクスポート
<div align="center">
<img src="3.png">
</div>


▼ データセットからエクスポート
<div align="center">
<img src="4.png">
</div>

#### PPTX ファイル
レポートのページを PowerPoint の各スライドに静的な画像としてエクスポートする “画像を埋め込む” と、PowerPoint スライドにライブ Power BI レポート ページを追加する “ライブ データを埋め込む” があります。
なお、“ライブ データを埋め込む” は、データが実際に PowerPoint ファイルの一部になることはありません。 データは Power BI 内でセキュリティで保護された状態に維持されます。


必要な権限：
閲覧権限を持っているユーザーにて操作可能です。

ご参考情報：
[レポートを PowerPoint にエクスポートする](https://learn.microsoft.com/ja-jp/power-bi/collaborate-share/end-user-powerpoint)
[PowerPoint にライブ Power BI レポート ページを追加する](https://learn.microsoft.com/ja-jp/power-bi/collaborate-share/service-power-bi-powerpoint-add-in-install?tabs=share)

<div align="center">
<img src="5.png">
</div>

#### PDF ファイル
表示しているページまたはレポート全体をPDFファイルにエクスポートできます。

必要な権限：
閲覧権限を持っているユーザーにて操作可能です。

ご参考情報：
[Power BI から PDF にレポートをエクスポートする](https://learn.microsoft.com/ja-jp/power-bi/consumer/end-user-pdf?tabs=powerbi-service)
<div align="center">
<img src="6.png">
</div>

#### MHTML ファイル、XML ファイル、DOCX ファイル
ページ分割されたレポートを MHTML、XML ファイル、DOCX ファイルにエクスポートできます。
※　ページ分割されたレポートは、Premium 容量または Premium Per User 容量でのみ利用可能です。

必要な権限：
閲覧権限を持っているユーザーにて操作可能です。

ご参考情報：
[Power BI Premium のページ分割されたレポートとは - ページ分割されたレポートを表示する](https://learn.microsoft.com/ja-jp/power-bi/paginated-reports/paginated-reports-report-builder-power-bi#view-your-paginated-report)
<div align="center">
<img src="7.png">
</div>

#### PNG ファイル
PNG のエクスポートは API を使用します。
なお、概要の exportToFile APIは Premium Gen2 容量でのみ使用できます。

必要な権限：
閲覧権限を持っているユーザーにて操作可能です。

ご参考情報：
[Power BI レポートをファイルにエクスポートする](https://learn.microsoft.com/ja-jp/power-bi/developer/embedded/export-to)
[Reports - Export To File](https://learn.microsoft.com/en-us/rest/api/power-bi/reports/export-to-file)
[Reports - Export To File In Group](https://learn.microsoft.com/en-us/rest/api/power-bi/reports/export-to-file-in-group)

#### 印刷
レポートを1ページずつ印刷できます。　　

必要な権限：
閲覧権限を持っているユーザーにて操作可能です。

ご参考情報：
[Power BI サービスから印刷する](https://learn.microsoft.com/ja-jp/power-bi/consumer/end-user-print)

#### その他ご参考：Excelで分析
［エクスポート］に表示される“Excelで分析” は、Power BI データセットを Excel に取り込み、ピボットテーブル、グラフ、スライサー、およびその他の Excel 機能を使用してデータセットを表示および操作できる機能です。
今回のテナント設定とは異なる設定で制御される機能となりますが、以下に参考となる公開情報をご案内いたします。

ご参考情報：
[Power BI で [Excel で分析] を使用して開始する](https://learn.microsoft.com/ja-jp/power-bi/collaborate-share/service-analyze-in-excel)

</br>

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)

