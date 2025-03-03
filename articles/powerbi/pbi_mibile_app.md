---
title: Power BI モバイル アプリについて
date: 2025-01-31 00:00:00 
tags:
  - Power BI
  - モバイル アプリ
  - mobile apps
  - Power BI サービス
  - Power BI Service
---
こんにちは、Power BI サポートチームの呂です。

ビジネスの現場では、必要なデータを素早く把握し、的確な判断を下すことが求められます。Power BI モバイル アプリを活用すれば、スマートフォンやタブレットから簡単にデータにアクセスでき、外出先でも最新のレポートやダッシュボードを確認できます。

本記事では、Power BI モバイル アプリの主な機能や活用方法、Power BI サービスとの違い、トラブルシューティングのポイントに加え、最新のバージョン更新情報について説明します。
公開情報：[Power BI モバイル アプリのドキュメント - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/consumer/mobile/)

<!-- more -->
> [!IMPORTANT]  
> 本記事編集時点と実際の機能に相違がある場合がございます。予めご了承ください。
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

</br>


## 目次
1. [Power BI モバイル アプリとは](#1-Power-BI-モバイル-アプリとは)
2. [モバイルに最適化されたレポートを作成する](#2-モバイルに最適化されたレポートを作成する)
3. [ホーム画面とナビゲーション](#3-ホーム画面とナビゲーション)
4. [Power BI モバイル アプリの主な機能](#4-Power-BI-モバイル-アプリの主な機能)
5. [モバイル アプリと Power BI サービスの違い](#5-モバイル-アプリと-Power-BI-サービスの違い)
6. [バージョン更新について](#6-バージョン更新について)
7. [トラブルシューティング](#7-トラブルシューティング)
8. [よくある質問（FAQ）](#8-よくある質問（FAQ）)

</br>

## 1.Power BI モバイル アプリとは
Power BI モバイル アプリは、Microsoft Power BI のレポートやダッシュボードをモバイルデバイスで閲覧・操作できるアプリです。
iOS と Android に対応しており、クラウドやオンプレミスのデータに接続し、分析を行えます。
公開情報：[Power BI モバイル アプリとは - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/consumer/mobile/mobile-apps-for-mobile-devices)

<div align="left">
<img src="1.png">
</div>

### 使用例
**営業担当者の外出先でのデータ確認**
営業担当者は、外出先でスマートフォンを使って Power BI モバイル アプリにアクセスし、最新の売上データや顧客情報をリアルタイムで確認できます。これにより、訪問前に顧客の購買履歴や契約状況を把握し、効果的な提案や商談が可能になります。

**現場マネージャーのリアルタイムモニタリング**
製造業の現場マネージャーは、タブレットで生産ラインの稼働状況や品質指標をリアルタイムで監視できます。異常が検知された場合、アラートを受け取り迅速に対応することで、生産効率の向上や不良品の削減につながります。

**経営者の迅速な意思決定支援**
経営者は、移動中でもスマートフォンやタブレットで Power BI モバイル アプリを活用し、会社の業績指標や財務データを確認できます。重要な会議や出張先でも、最新の情報をもとに迅速な意思決定が可能になります。

</br>

## 2.モバイルに最適化されたレポートを作成する
コンピューター向けのレポートは、スマートフォンでは閲覧や操作がしにくい場合があります。
Power BI では、モバイル専用のページを作成し、画面サイズに最適化した縦長レイアウトを設計することで、スマートフォンやタブレットでも見やすく、直感的に操作できるレポートを提供できます。
公開情報：[モバイル最適化 Power BI レポートについて - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/create-reports/power-bi-create-mobile-optimized-report-about)
<div align="left">
<img src="2.png">
</div>
</br>
モバイル最適化されたページを含むレポートは、Power BI モバイル アプリ内で特別なアイコンで示されます。
<div align="left">
<img src="3.png">
</div>

</br>

## 3.ホーム画面とナビゲーション
Power BI モバイル アプリのホーム画面では、以下３つのタブを切り替えることができます。
**クイックアクセス:** 最近表示したレポートや、推奨されるコンテンツにすばやくアクセスできます。
**メトリックハブ:** 関連するメトリックが示され、スコアカードの一覧を確認できます。
**アクティビティフィード:** Power BI のコンテンツ更新やコメント追加などのアクティビティを確認できます。
公開情報：[モバイル アプリのホーム ページの概要 - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/consumer/mobile/mobile-apps-home-page)
<div align="left">
<img src="4.png">
</div>
画面の下に表示されるナビゲーションバーでは、以下の機能に簡単にアクセスできます。
<div style="display: flex; align-items: center;">
  <img src="home-icon.png" alt="" width="20" height="20" style="margin-right: 5px; border: none;">
  <strong>ホーム</strong> - ホームページに戻ります。
</div>

<div style="display: flex; align-items: center;">
  <img src="favorite-icon.png" alt="" width="20" height="20" style="margin-right: 5px; border: none;">
  <strong>お気に入り</strong> - お気に入りとしてマークしたレポート、ダッシュボード、アプリ。
</div>

<div style="display: flex; align-items: center;">
  <img src="app-icon.png" alt="" width="20" height="20" style="margin-right: 5px; border: none;">
  <strong>アプリ</strong> - ご自分のアカウントにインストールされているアプリ。
</div>

<div style="display: flex; align-items: center;">
  <img src="workspace-icon.png" alt="" width="20" height="20" style="margin-right: 5px; border: none;">
  <strong>ワークスペース</strong> - コンテンツ作成者が作成しているレポートとダッシュボードがまとめて保持されている作業フォルダー。
</div>

<div style="display: flex; align-items: center;">
  <img src="recent-icon.png" alt="" width="20" height="20" style="margin-right: 5px; border: none;">
  <strong>最近使用</strong> - 最近表示した項目。
</div>

<div style="display: flex; align-items: center;">
  <img src="shared-icon.png" alt="" width="20" height="20" style="margin-right: 5px; border: none;">
  <strong>自分と共有</strong> - 他のユーザーが自分と共有した項目。
</div>

<div style="display: flex; align-items: center;">
  <img src="explore-icon.png" alt="" width="20" height="20" style="margin-right: 5px; border: none;">
  <strong>探索</strong> - 特に自分向けに選択された、組織のコンテンツ。
</div>

<div style="display: flex; align-items: center;">
  <img src="notification-icon.png" alt="" width="20" height="20" style="margin-right: 5px; border: none;">
  <strong>通知</strong> - 通知を表示したり、アクセスしたりすることができます。
</div>

</br>

## 4.Power BI モバイル アプリの主な機能

### ダッシュボードとレポートの閲覧
Power BI サービスと連携し、クラウド上に保存されたダッシュボードやレポートをスマートフォンやタブレットで確認できます。視覚的なデータ分析を行いながら、重要な指標をリアルタイムで把握することが可能です。

### フィルターとスライサーを利用したデータ分析
モバイル アプリでも、フィルターやスライサーを使用してデータを絞り込むことができます。ブラウザ版と同様に、特定の期間やカテゴリにフォーカスした分析を簡単に行えます。

### オフラインモード
ネットワーク接続がない環境でも、Power BI モバイル アプリは一部のデータをキャッシュし、オフラインでの閲覧をサポートします。これにより、移動中や通信環境が不安定な場所でも重要な情報を確認できます。

### アラート機能
データが特定の条件を満たした際に通知を受け取ることができます。例えば、売上が一定の閾値を超えた場合に通知を設定しておけば、すぐに状況を把握し、適切な対応を講じることが可能になります。

### 共有とコラボレーション
Power BI モバイル アプリを使用すると、ダッシュボードやレポートを同僚と共有したり、コメントを追加してフィードバックをやり取りできます。これにより、チームメンバーとの円滑な情報共有が可能になります。

</br>

## 5.モバイル アプリと Power BI サービスの違い
Power BI モバイル アプリは閲覧に特化しており、Power BI サービスのようなレポート作成やデータモデリングはできません。  
一方で、タッチ操作に最適化されており、外出先でもリアルタイムで情報を確認するのに適しています。

| 機能 | ブラウザ版 | モバイル アプリ |
|------|----------|---------------|
| レポート・ダッシュボード閲覧 | ◯ | ◯ |
| レポートの作成・編集 | △（一部の操作は Power BI Desktop が必要） | ✕ |
| オフライン閲覧 | ✕（ネットワーク接続が必須） | ◯（一部のデータをキャッシュして閲覧可能） |
| タッチ操作最適化 | △（操作は可能だが、PC向けの UI 設計） | ◯（タッチ操作に最適化された UI） |
| ユーザーアクセス管理 | ◯ | △（一部の設定はモバイルアプリでは制限あり） |
| 管理者操作 | ◯（詳細な管理機能が利用可能） | ✕（管理者向け機能は利用不可） |
| データの更新 | ◯ | ◯ |
| データのエクスポート | ◯（Excel や CSV にエクスポート可能） | ✕ |

</br>

## 6.バージョン更新について
Power BI モバイル アプリは、毎月新しいバージョンがリリースされ、新機能の追加やバグ修正、パフォーマンスの向上が継続的に行われています。最新の更新情報や過去の更新履歴については、[公開情報](https://learn.microsoft.com/ja-jp/power-bi/consumer/mobile/mobile-whats-new-in-the-mobile-apps)をご確認ください。

</br>

## 7.トラブルシューティング
モバイル アプリで問題が発生し、お問い合わせいただく際は以下の調査を行い、情報を提供いただくことで、スムーズな調査が可能になります。
１．最新版のモバイル アプリで事象が再現するかをご確認ください。
２．ご利用のデバイスと OS の詳細をお知らせください。
３．一度アプリをアンインストールし、再度インストール後、事象が再現するかご確認ください。
４．同じ端末のブラウザで Power BI サービスにアクセスし、事象が再現するかを確認してください。
　　サポートされているブラウザの詳細は、以下の公式情報をご確認ください。
　　公開情報：[Power BI と Farbic のサポートされているブラウザー - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/fundamentals/power-bi-browsers)
６．問題が発生する際の画面録画を採取します。
７．録画後、ユーザーアイコン > [Settings] を選択し、下へスクロールして "Version" および "Session ID" を確認します。

</br>

## 8.よくある質問（FAQ）

**Q1:** Power BI モバイル アプリはどのデバイスで利用できますか？
**A1:** 2025年1月時点では、iOS/iPadOS 16.4 以降および Android 8.0 以降のデバイスで利用できます。

**Q2:** Power BI モバイル アプリは無料で利用できますか？
**A2:** Power BI モバイル アプリは無料でダウンロードや利用できます。  
ただし、レポートやダッシュボードへのアクセスには、組織の Power BI ライセンスが必要な場合があります。

**Q3:** モバイル アプリのセキュリティ対策はどのようになっていますか？
**A3:** Power BI モバイル アプリは、データの暗号化や認証プロセスを通じて、データのセキュリティとプライバシーを確保しています。詳細は[公開情報](https://learn.microsoft.com/ja-jp/power-bi/guidance/whitepaper-powerbi-security?utm_source=chatgpt.com#power-bi-mobile)をご参照ください。

</br>

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---
**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)