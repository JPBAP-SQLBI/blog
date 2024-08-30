---
title: Power BI 新規機能のご紹介（2024年5月～ 7月）
date: 2024-08-30 00:00:00 
tags:
  - Power BI
  - Power BI Desktop
  - Power BI サービス
  - New Feature  
  - 新機能
  - DAX query view
  - DAX クエリ ビュー
  - Manage relationships
  - リレーションシップの管理
  - Download large semantic models
  - 大規模なセマンティック モデルのダウンロード
  - Row-level security 
  - 行レベルセキュリティ（RLS）
---


こんにちは、Power BI サポート チームのファムです。

Power BI公式の製品ブログにて毎月新しい機能が紹介されていることをご存じでしょうか。Power BIは最新のバージョンのみをサポートしておりますので、Power BI Desktopバージョンの最新化を心がけましょう。

本ブログでは、2024年5月～7月のPower BI公式の製品ブログに紹介された一部の新機能をご紹介いたします。

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
1. [はじめに](#1．はじめに)
2. [DAX クエリ ビュー 「５月ブログ」](#2．DAX-クエリ-ビュー-「５月ブログ」)
3. [新しい「リレーションシップの管理」 ダイアログ 「５月ブログ」](#3．新しい「リレーションシップの管理」-ダイアログ-「５月ブログ」)
4. [大規模なセマンティック モデルのダウンロード 「６月ブログ」](#4．大規模なセマンティック-モデルのダウンロード-「６月ブログ」)
5. [Power BI Desktopの拡張行レベル セキュリティ エディターの一般提供開始 「７月ブログ」](#5．Power-BI-Desktopの拡張行レベル-セキュリティ-エディターの一般提供開始-「７月ブログ」)
</br>

---

## 1．はじめに

Power BI公式の製品ブログでは、製品や機能リリースに関する最新情報を紹介しております。今回はその中から、皆さんのお役に立ちそうな新機能をいくつかピックアップし、本ブログにてご紹介いたします。
今回紹介しているブログはこちらのサイトからもご確認できます。

//公開情報：[Power BI ブログ — 更新とニュース](https://powerbi.microsoft.com/ja-jp/blog/)

Power BI DesktopとPower BI サービスに対する過去の月次更新は、以下の公開情報にまとめていますので、過去のバージョンの機能をご確認されたい場合、ぜひご参照してください。

//公開情報：[Power BI Desktop と Power BI サービスに対する過去の月次更新](https://learn.microsoft.com/ja-jp/power-bi/fundamentals/desktop-latest-update-archive?tabs=powerbi-desktop)
//参考情報：[Power BI のアップデート情報について](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_feature_roadmap/#Power-BI-Desktop-%E3%83%BB-Power-BI-%E3%82%B5%E3%83%BC%E3%83%93%E3%82%B9)

今回紹介している一部の機能は、以下のブログをご確認ください。

//５月のブログ：[Power BI May 2024 Feature Summary](https://powerbi.microsoft.com/ja-jp/blog/power-bi-may-2024-feature-summary/#post-27048-_Toc167109006)
//６月のブログ：[Power BI June 2024 Feature Summary](https://powerbi.microsoft.com/ja-jp/blog/power-bi-may-2024-feature-summary/#post-27048-_Toc167109006)
//７月のブログ：[Power BI July 2024 Feature Summary](https://powerbi.microsoft.com/ja-jp/blog/power-bi-july-2024-feature-summary/#post-27650-_Toc1615654178)


## 2．DAX クエリ ビュー 「５月ブログ」

DAX クエリは、セマンティック データ モデルからすばやく探索して分析情報を得るのに役立ちます。例えば、DirectQueryの場合、「**データビュー**」が表示されていないので、こちらの「**DAX クエリ ビュー**」を活用すれば、テーブルをご確認いただけます。データ ペインの項目を右クリックして、上位 100 行などの DAX クエリを生成し、データ列に値を表示することができます。

</br>

<div align="center">
<img src="pic1.png">
</div>


//公開情報：[DAX クエリ ビュー](https://learn.microsoft.com/ja-jp/power-bi/transform-model/dax-query-view)

</br>

## 3．新しい「リレーションシップの管理」 ダイアログ 「５月ブログ」

新しい「**リレーションシップの管理**」 では、すべての関係とその主要なプロパティの包括的なビューが1 つの便利な場所に表示されます。ここから、新しいリレーションシップを作成したり、既存のリレーションシップを編集したりできます。
❶カーディナリティとクロス フィルターの方向に基づいて、モデル内の特定のリレーションシップのフィルターを処理できます。
❷また、Power BI では 「**自動検出**」 ボタンを選択することで、リレーションシップを見つけて作成できます。

</br>

<div align="center">
<img src="pic2.png">
</div>

</br>

## 4．大規模なセマンティック モデルのダウンロード 「６月ブログ」

大規模なセマンティック モデルを .pbix ファイルとして Power BI Desktop にダウンロードできるようになりました。大規模なセマンティック モデル ストレージ形式に対して有効になっているセマンティック モデルに基づくレポートを同時にダウンロードしようとするとエラーが発生する恐れがあります。また、REST APIを使用してダウンロードできませんので、ご留意ください。

</br>

<div align="center">
<img src="pic3.png">
</div>

</br>

//公開情報：[Power BI サービスから Power BI Desktop にレポートをダウンロードする](https://learn.microsoft.com/ja-jp/power-bi/create-reports/service-export-to-pbix)

</br>


## 5．Power BI Desktopの拡張行レベル セキュリティ エディターの一般提供開始　「７月ブログ」

Power BI Desktop の拡張された行レベルのセキュリティ エディターの一般提供が開始されました。このエディターを使用すると、行レベルのセキュリティ ロールとフィルターをすばやく簡単に作成できます。リボンから「**ロールの管理**」を選択するだけで、エディターが開きます。

</br>

<div align="center">
<img src="pic4.png">
</div>

</br>


デフォルトでは、DAX を記述しなくても、セキュリティロールを作成および編集するための使いやすいドロップダウンインターフェイスが開きます。

</br>

<div align="center">
<img src="pic5.png">
</div>

</br>

DAX を使用する場合、またはフィルター定義に DAX が必要な場合は、DAX エディターを使用してロールを定義するように切り替えることができます。

</br>

<div align="center">
<img src="pic6.png">
</div>

</br>


詳細については、下記の公開情報を併せてご参照ください。

//公開情報：[Power BI での行レベルのセキュリティ (RLS)](https://learn.microsoft.com/ja-jp/fabric/security/service-admin-row-level-security)


**最後に：**
冒頭でもご案内した通り、Power BI Desktopは毎月新機能が追加されます。また、既存機能の修正やアップデート等も含まれるため、Microsoftでは最新版Power BI Desktopのみをサポート対象としております。
このため、常に最新版のPower BI Desktopをご利用いただくことをご検討ください。
以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。


</br>
以上、本ブログ が少しでも皆様のお役に立てますと幸いでございます。


---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)
