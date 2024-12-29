---
title: Teams アクティビティ分析レポートの廃止について（MC907531）
date: 2024-12-27 00:00:00 
tags:
  - Power BI
  - Teams 
  - Power BI サービス
---

こんにちは、Power BI サポート チームの呂です。

「Teams アクティビティ分析レポート」機能は、2025 年 1 月 31 日をもって正式に廃止されます。2025 年 2 月 1 日以降、ユーザーはこの機能を利用して新しいレポートを作成できなくなり、既存のレポートは更新されなくなります。
本ブログでは、本機能廃止の背景、影響、および代替機能についてご案内いたします。

> [!TIP]
> 参考情報：[Teams 用 Power BI アプリで Teams の利用状況を分析する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/collaborate-share/service-teams-analytics)
> 参考情報：[Power BI in Teams – ‘Teams activity analytics’ report deprecation | Microsoft Power BI ブログ | Microsoft Power BI](https://powerbi.microsoft.com/ja-jp/blog/power-bi-in-teams-teams-activity-analytics-report-deprecation/)

## Teams アクティビティ分析レポート機能はどんな機能であるか

「Teams アクティビティ分析レポート」は、ユーザーが自身のワークスペース内で作成できる標準のレポートであり、Teams の利用データを追跡するためのツールです。

Teams アクティビティ分析レポートは以下の 3 つのタブが含まれています：
・マイ アクティビティ ページ： Teams での最近のアクティビティの概要を表示します
・チーム アクティビティ ページ： 所属するすべてのチームとそのアクティビティを一覧表示します
・チーム アクティビティの詳細： 所属する Teams チームの過去 90 日間のアクティビティを表示します

<div align="left">
<img src="1.png">
</div>
</br>

## Teams アクティビティ分析レポートの廃止理由
Teams では、チームやチャネルの利用状況を分析できるネイティブな分析ビューが提供されています。この機能により、アクティブユーザー数、投稿数、返信数といったチーム内の活動データを簡単に把握することができます。
この分析ビューは、Teams の利用状況をより包括的に把握するための新しい機能の一部として提供されています。この新しい機能を使うことで、チャネルやチャットを通じたユーザー間のコミュニケーション状況や、接続デバイスの種類など、従来よりも広範囲で詳細なデータを確認することができます。
※本機能の詳細については、「今後の代替機能」で紹介する公開情報をご参照ください。

こうした包括的な分析を可能にする新しいツールの提供に伴い、「Teams アクティビティ分析レポート」の役割が限定的となり、その必要性が薄れたため、廃止されることになりました。
</br>

## 今回の変更が与える影響
2025 年 2 月 1 日から、作成済み「Teams アクティビティ分析」レポートは、廃止後に更新されなくなります。
Power BI アプリの「作成」セクションから「Teams アクティビティ分析」レポートを新規作成するオプションも削除され、今後新たこのレポートを作成することはできなくなります。
</br>

## 今後の代替機能
組織内で Teams の利用状況を把握する必要がある場合は、Teams が提供する「Teams Analytics」機能をご利用ください。
詳細については、以下のドキュメントをご覧ください：
[Microsoft Teamsでチームの分析を表示する - Microsoft サポート](https://support.microsoft.com/ja-jp/office/microsoft-teams-%E3%81%A7%E3%83%81%E3%83%BC%E3%83%A0%E3%81%AE%E5%88%86%E6%9E%90%E3%82%92%E8%A1%A8%E7%A4%BA%E3%81%99%E3%82%8B-5b8ad4b1-af34-4217-aff4-cd11a820b56b)
</br>


以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)