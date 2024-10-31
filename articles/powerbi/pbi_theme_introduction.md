---
title: Power BI テーマについて
date: 2023-02-28 00:00:00 
tags:
  - Power BI
  - テーマ
  - theme
  - Power BI サービス
  - Power BI Service
  - Power BI Desktop
---
こんにちは、Power BI サポート チームの呂です。
レポートやダッシュボードのデザインを一括で設定する方法として、Power BI テーマという便利な機能があることをみなさんご存知でしょうか？
今回は、Power BI テーマの機能や利用方法について紹介します。

<!-- more -->
> [!IMPORTANT]  
> 本記事編集時点と実際の機能に相違がある場合がございます。予めご了承ください。
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
## 目次
---
1. [Power BIのテーマとは](#Power-BI-のテーマとは)
2. [レポートテーマの設定方法](#レポートテーマの設定方法)
3. [カスタムダッシュボードテーマ](#カスタムダッシュボードテーマ)
4. [Power BIテーマの運用方法](#Power-BIテーマの運用方法)
5. [テーマギャラリー](#テーマギャラリー)
</br>

---
## Power BI のテーマとは
---

Power BIのテーマ機能を使用すると、コンテンツの全体にデザインが適用され、すべてのビジュアルで設定されたテーマの色や文字の書式が既定値として使用されます。
テーマ機能は現在、レポートとダッシュボードに設定できますが、本ブログは主にレポートでのテーマ設定を中心に紹介していきます。

### テーマ設定のメリット
・既定で選択できないフォントを使用可能になります
<div align="left">
<img src="1.png">
</div>

・既定で選択できる[テーマの色]を変更できます
<div align="left">
<img src="2.png">
</div>

・組織内で使用されるレポートのデザインを統一できます

・レポートやビジュアルのデザインを一括設定することで工数が減ります　など
<br>

---
## レポートテーマの設定方法
---

Power BI Desktop の レポートテーマは、[表示]リボンのテーマセクションから、以下3つの方法で設定することが可能です。
①	組み込み：既定のテーマがございますのでそのまま使用可能
②	カスタム：一般的なレポートテーマのオプションをカスタマイズ可能
③	JSON：カスタム設定よりさらに細かな制御が可能
<div align="left">
<img src="3.png">
</div>

### カスタム設定で指定可能な内容

■名前と色
テーマの色：レポートで主に使用される色
センチメントの色：正、負、または中立の結果を示すために、主要業績評価指標 (KPI) のビジュアルとウォーターフォール図で使用される色
分岐の色：データポイントが範囲内かどうかを示すために条件付き書式設定で使用される色
構造色 ：ビジュアル要素の軸グリッド線、強調表示色、背景色など
> [!TIP]
> 参考情報：[Power BI Desktop でレポート テーマを使用する - Power BI | Microsoft Learn―構造色を設定する](https://learn.microsoft.com/ja-jp/power-bi/create-reports/desktop-report-themes#set-structural-colors)

■テキスト
全般（データと軸ラベルを含む各視覚エフェクト）、タイトル（各ビジュアルの主要なタイトルと軸のタイトル）、カードとKPIのコールアウト値、主要なインフルエンサービジュアルのタブヘッダーのテキストフォント、サイズ及び色を設定できます。

■ビジュアル
背景：背景色や透明度を設定できます。
罫線：色や半径を設定できます。
ヘッダー：各ビジュアルの上部領域の背景色、枠線やアイコンの色、透明度を設定できます。
ツールヒント：背景色、ラベルや値のテキストの色を設定できます。
> [!TIP]
> 参考情報：[Power BI Desktop でのヒントのカスタマイズ - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/create-reports/desktop-custom-tooltips)

■ページ
[壁紙]及び[ページの背景]の背景色や透明度を設定できます。

■フィルター
[フィルターウィンドウ]、[使用可能なフィルターカード]及び[適用されたフィルターカード]の背景色、透明度、フォントとアイコンの色やサイズを設定できます。

### JSONでレポートテーマを細かく制御する

カスタム設定で指定できない内容については、JSONで設定行うことで、より細かな制御を実現できます。例えば既定では選択可能なフォントが限られた数や種類しかありませんので、レポートで日本語を使用する際にフォントにこまることはありませんか。Power BIテーマを設定することで、既定のリストに存在しない日本語のフォントに簡単に変えることができます。

例えば、以下のJSONを使用することで、レポートのすべての文字フォントを”Meiryo”に指定することができます。

```json
{
    "name": "CustomTheme",
    "textClasses": {
        "callout": {
            "fontFace": "Meiryo"
        },
        "header": {
            "fontFace": "Meiryo"
        },
        "title": {
            "fontFace": "Meiryo"
        },
        "largeTitle": {
            "fontFace": "Meiryo"
        },
        "label": {
            "fontFace": "Meiryo"
        },
        "semiboldLabel": {
            "fontFace": "Meiryo"
        },
        "largeLabel": {
            "fontFace": "Meiryo"
        },
        "smallLabel": {
            "fontFace": "Meiryo"
        },
        "lightLabel": {
            "fontFace": "Meiryo"
        },
        "boldLabel": {
            "fontFace": "Meiryo"
        },
        "largeLightLabel": {
            "fontFace": "Meiryo"
        },
        "smallLightLabel": {
            "fontFace": "Meiryo"
        }
    }
}
```

JSONの作成方法ですが、Power BI では"JSON スキーマ" に基づいてカスタムテーマが検証されます。そのため、設定可能な項目などを確認するには、テーマの設定に使用できるプロパティを"JSON スキーマ"をGitHubから取得して、ご確認いただく必要がございます。
> [!TIP]
> 参考情報：[Report Theme JSON Schema at main · microsoft/powerbi-desktop-samples · GitHub](https://github.com/microsoft/powerbi-desktop-samples/tree/main/Report%20Theme%20JSON%20Schema)

また、"JSON スキーマ"を確認しても、実際な設定につまずくこともあるかもしれません。以下のGitHubページでは、ビジュアルごとにテーマを設定したサンプルコードを用意しておりますため、ご参照いただけますと幸いです。

> [!TIP]
> 参考情報：[PowerBI-ThemeTemplates/README.md at master · MattRudy/PowerBI-ThemeTemplates · GitHub](https://github.com/mattrudy/PowerBI-ThemeTemplates/blob/master/README.md)

なお、以下の公開情報に、基本なJSON構文やすぐご利用可能な例文が紹介されておりますで、必要に応じてご活用ください。

> [!TIP]
> 参考情報：[Power BI Desktop でレポート テーマを使用する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/create-reports/desktop-report-themes)

---
## カスタムダッシュボードテーマ
---

Power BIレポートに適用するテーマは、ダッシュボードにも適用することができます。 既にレポート テーマが適用されているレポートからのタイルをピン留めする場合は、現在のテーマを保持するか、ダッシュボード テーマを使用するかを選択できます。
以下画面ショットの通り、ダッシュボード画面から[編集]＞[ダッシュボード テーマ]から、JSONのアップロードや、カスタムテーマの設定が可能です。
※ダッシュボードのカスタムテーマは、レポートからピン留めされたタイルでのみ機能します。

<div align="left">
<img src="4.png">
</div>

> [!TIP]
> 参考情報：[Power BI サービスのダッシュボード テーマを使用する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/create-reports/service-dashboard-themes)

---
## Power BIテーマの運用方法
---

レポートテーマを作成したあとの運用方法は、JSONファイルや、テンプレートレポートで運用する方法をご紹介します。

### JSONでの運用

JSON スキーマをもとに作成したJSONファイル、もしくはテーマのカスタマイズを行い適用したあとに、[現在のテーマを保存]を選択することで、JSONファイルとしてエクスポートして運用できます。JSONで運用する場合、すでに作成済のレポートや、ダッシュボードにも適用することも可能で、様々な場面に対応できる運用方法となっております。

<div align="left">
<img src="5.png">
</div>

### テンプレートレポートでの運用

一方、JSON運用を行う場合は、ユーザーに参照する手順の説明が必要など、運用が難しい場合は、Power BIのテンプレートレポートでの運用もございます。
以下画面ショットのとおり、レポートをテンプレートレポート(.pbitファイル)としてエクスポートすることが可能です。エクスポートされた.pbitファイルは、データやクエリの定義や、ビジュアルやテーマの定義が含まれますが、データは含まれず、手軽に共有できるサイズになります。.pbitファイルをユーザーに共有して運用をすることで、ユーザーは、設定されているテーマをベースにレポートを作成できますので、レポートにJSONを適用する手間はありません。

<div align="left">
<img src="6.png">
</div>

> [!TIP]
> 参考情報：[Power BI Desktop でレポート テーマを使用する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/create-reports/desktop-report-themes#setting-structural-colors)

---
## テーマギャラリー
---

Power BI コミュニティサイトは、世界中にいるさまざまなPower BIのエンジニアや有識者にて運営されており、お互いにPower BIの課題を解決し合う場となっております。
そのコミュニティサイトに、ユーザーの皆様がご作成、ご共有いただきましたPower BIが、テーマギャラリーでシェアされています、レポートのデザインを行う際にご参照いただけますと幸いでございます。

> [!TIP]
> 参考情報：[Themes Gallery - Microsoft Power BI Community](https://community.powerbi.com/t5/Themes-Gallery/bd-p/ThemesGallery)

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)