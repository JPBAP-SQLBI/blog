---
title: Power BI とData Activator のデータアラート機能の比較
date: 2024-05-31 00:00:00 
tags:
  - Power BI サービス
  - Data Activator
  - データアラート
  - Fabric
---


こんにちは、Power BI サポート チームの中川です。

Power BI では、データが変化したときにユーザーに通知するアラート機能があります。Microsoft Fabric の Data Activator にも同様の機能が実装されたことにより、「両者機能がどう違うのか」、「どのように使い分けるべきか」と悩まれている方も多いかと思います。

本ブログでは、 Power BI と Data Activator のアラート機能の違いや、それぞれの効果的な活用方法についてご紹介いたします。

<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
## 目次
---
* [アラート機能とは](#アラート機能とは)
* [アラート機能の比較表](#アラート機能の比較表)
* [リリース状況](#リリース状況)
* [必要なライセンス、テナント設定](#必要なライセンスとテナント設定)
* [対象アイテムと対象ビジュアル](#対象アイテムとビジュアル)
* [通知方法と Power Automate 連携](#通知方法と-Power-Automate-連携)
* [通知対象ユーザー](#通知対象ユーザー)
* [ゲストユーザーを受信者とした設定](#ゲストユーザーを受信者とした設定)
* [通知タイミングおよびトリガーできるデータ型と条件](#通知タイミングおよびトリガーできるデータ型と条件)
* [作成方法および管理方法](#作成方法および管理方法)
* [おわりに](#おわりに)



---
## アラート機能とは
---
アラート機能は、レポートまたはダッシュボードに対して、特定のデータのしきい値を設定し、その条件を満たした際に通知を送る機能です。
例えば、売上が目標に達しなかった場合や在庫が一定の水準を下回った場合に通知を受け取ることで、業務フローや日々のオペレーションに対して迅速な対応に役立ちます。
また、 Microsoft Power Automate と連携させることで、通知をトリガーとして様々なアクションを実行することが可能です。


---
## アラート機能の比較表
---

Power BI と Data Activator の両方でデータアラート機能が提供されていますが、それぞれの特長や用途には違いがあります。</br>
まずはこれらの違いを表形式でまとめ、以降の章では各項目について詳しく解説していきます。

| 機能 | Power BI データアラート | Data Activator |
|---|---|---|
| リリース状況 | リリース済み | パブリックプレビュー中 |
 必要なライセンス</br> （アクセス可能なワークスペースで利用可能） | <ul><li>マイ ワークスペース</li><li>Premium 容量</li><li>Power BI Pro</li><li>Premium Per User (PPU)</li></ul>  | <ul><li>Premium 容量</li><li>Fabric 容量</li><li>Fabric 試用版</li></ul> |
| テナント設定 | 不要 | [ Data Activator (プレビュー) ] を有効にする |
| 対象アイテム | ダッシュボード | レポート |
| 対象ビジュアル | ゲージ、KPI、カード | 多くのビジュアルに対応 |
| 通知方法 | メール、Teams（要Power Automate連携） | メール、Teams |
| Power Automate連携 | 〇 | 〇 |
| 通知対象 | 作成者のみ | Fabricテナントに属するユーザー |
| ゲストユーザーを受信者とした設定 | 〇 | × |
| 通知タイミング | 1時間に1回または24時間に1回 | 条件が満たされるたび |
| トリガーできるデータ型 | 数値のみ | 数値のみ |
| 設定できる条件 | 閾値超過時に通知可能 | 閾値超過時、回数、値の範囲など |
| 作成方法 | 数クリックで作成可能 | 数クリックで作成可能 |
| 管理方法 | ダッシュボード タイルまたは設定メニューから | reflexアイテムで管理 |


---
## リリース状況
Power BI のデータアラート機能はすでに正式にリリース（GA）されていますが、 Data Activator は現在プレビュー段階にあります。</br>
プレビュー段階の機能は、今後予告なしに機能が削除されたり、動作変更が発生する可能性があります。また、公開情報に記載されていない制限事項が存在する場合もございます。</br>
そのため、プレビュー機能を使用する際には、これらの点に留意してご利用いただけますようお願いします。


>[!NOTE]
> 参考情報：[プレビュー使用条件 | Microsoft Azure](https://azure.microsoft.com/ja-jp/support/legal/preview-supplemental-terms/#AzureOpenAI-PoweredPreviews)

本ブログの情報は記事執筆時点のものであり、詳細については最新の公開ドキュメントをご参照ください。

---
## 必要なライセンスとテナント設定

### Power BI データアラート
Power BI のデータアラート機能は、以下のいずれかのライセンスモードのワークスペースにアクセスできるユーザーが利用可能です。</br>
- マイ ワークスペース
- Premium 容量（Premium Per Capacity）
- Power BI Pro
- Premium Per User (PPU) 

これらのワークスペースにアクセスできるユーザーは、そのワークスペース内のダッシュボードに対しデータアラートを設定することができます。

> [!NOTE]
> 参考情報 ：[Power BI サービス ダッシュボードでデータ アラートを設定するためのチュートリアル。 - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/consumer/end-user-alerts#who-can-set-alerts)


### Data Activator
Data Activator は Microsoft Fabric 内のサービスであるため、Premium ライセンスまたは Fabric ライセンスが必要となります。
また、Fabric 試用版を有効にすることで Data Activator をお試しいただくことも可能です。

> [!NOTE]
> 参考情報 ：[Power BI から Data Activator のデータを取得する - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/data-activator/data-activator-get-data-power-bi#prerequisites)
> 参考情報 ：[Fabric 試用版の容量 - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/get-started/fabric-trials)


ライセンスの他に、テナント設定から [ Data Activator (プレビュー) ] を有効にする必要があります。

<div align="center">
<img src="Tenant Settings Data Activator.png">
</div>


なお、テナント設定の項目 [ ユーザーは Fabric アイテムを作成できます ] は、正式リリース済みの Fabric コンポーネント（Data Engineering、Data Warehouse 等）の Fabric アイテムの作成を制御する設定であり、プレビュー中の Data Activator は制御するコンポーネントの対象外となります。</br>
つまり、 [ ユーザーは Fabric アイテムを作成できます ] が無効となっている場合でも、[ Data Activator (プレビュー) ] が有効となっていれば、 Data Activator を利用いただくことが可能です。

<div align="center">
<img src="Tenant Settings Users can create Fabric items.png">
</div>

設定手順や詳細については、以下のリンクをご参照ください。
> [!NOTE]
> 参考情報 ：[Data Activator を有効にする - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/admin/data-activator-switch)
> 参考情報 ：[Power BI から Data Activator のデータを取得する - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/data-activator/data-activator-get-data-power-bi#prerequisites)



それぞれのライセンスの違いについて以下の弊社公開ブログをご参照ください。
> [!NOTE]
> 参考情報 ：[Power BI ライセンスの違い（Free・Pro・Premium Per User・Premium Per Capacity・Embedded・Fabric） | Japan CSS Support Power BI Blog (jpbap-sqlbi.github.io)](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_license/)


---
## 対象アイテムとビジュアル

### Power BI データアラート
Power BI データアラート では、レポートのビジュアルからピン留めされたダッシュボードタイルの以下のビジュアルに対してのみ設定が可能です。
- ゲージ
- KPI
- カード

> [!NOTE]
> 参考情報 ： [Power BI サービスでデータ アラートを設定する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/create-reports/service-set-data-alerts)

### Data Activator
Data Activator データアラートでは、レポート自体に対して直接アラートを設定することが可能です。さらに、対応するビジュアルの種類も多岐にわたるため、より広範なデータ監視と通知が可能です。

| サポートされる Power BI ビジュアル | | |
|:---:|:---:|:---:|
| 積み上げ列 | 集合縦棒 | 積み上げ横棒 |
| 100% 積み上げ縦棒 | 100% 積み上げ横棒 | 集合横棒 |
| リボン グラフ | 折れ線 | 面グラフ |
| 積み上げ面 | 折れ線および積み上げ縦棒 | 折れ線および集合縦棒 |
| Pie | ドーナツ | ゲージ |
| Card | KPI | Bing マップ |
| 塗り分け地図 | Azure マップ | ArcGIS マップ |



詳細については、以下のリンクをご参照ください。

> [!NOTE]
> 参考情報：[Data Activator の制限事項 - Microsoft Fabric | Microsoft Learn ](https://learn.microsoft.com/ja-jp/fabric/data-activator/data-activator-limitations#supported-power-bi-visuals)



---
## 通知方法と Power Automate 連携


### Power BI データアラート
Power BI データアラート では、通知センターにアラートを送信する以外には、メールのみ送信が可能です。

> [!NOTE]
> 参考情報：[Power BI サービスでデータ アラートを設定する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/create-reports/service-set-data-alerts#receive-alerts)



しかし、Power Automate を利用することで、Teams やその他のアクションを組み合わせて通知を送信することが可能です。

> [!NOTE]
> 参考情報：[Power BI データ アラートを Power Automate と統合する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/collaborate-share/service-flow-integration?source=recommendations)
> 参考情報：[PowerBI のアラートをチームに通知する | Microsoft Power Automate](https://powerautomate.microsoft.com/ja-jp/templates/details/d3ea3143c7634106b20952709e52af95/notify-a-team-of-powerbi-alerts/)


### Data Activator
Data Activator データアラート では、標準機能でメールまたは Teams 送信が可能です。また、カスタム アクションを使用して Power Automate フローをトリガーできるため、メールおよび Teams 以外のシステムを使用して通知を送信することもできます。

> [!NOTE]
> 参考情報：[カスタム アクションを使用して Power Automate フローをトリガーする - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/data-activator/data-activator-trigger-power-automate-flows)


---
## 通知対象ユーザー

### Power BI データアラート
Power BI データアラート では、ご自身が設定したアラートのみ確認できます。他者が作成したアラートを見ることはできません。

> [!NOTE]
> 参考情報：[Power BI サービス ダッシュボードでデータ アラートを設定するためのチュートリアル。 - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/consumer/end-user-alerts#who-can-see-alerts-i-create)



### Data Activator
Data Activator データアラート では、Fabric テナントに属するユーザー（個人またはMicrosoft 365 グループ）に送信することが可能です。外部メールアドレスまたはゲストメール アドレスにメールアラートを送信することはできませんのでご注意ください。</br>
なお、Microsoft 365 グループへ送信する場合は、設定から [ 組織外のユーザーによるこのチームへのメール送信を許可する ] を有効にする必要があります。


<div align="center">
<img src="M365_Allow users outside the organization to send email.png">
</div>


---
## ゲストユーザーを受信者とした設定

### Power BI データアラート
Power BI データアラート では、ゲストユーザーとして招待したユーザーがダッシュボードにアクセスが可能な場合、アラートの作成が可能です。</br>
ゲストユーザーとして招待する方法については以下のブログをご参照ください。

> [!NOTE]
> 参考情報：[組織外のユーザーとPower BIコンテンツの共有 | Japan CSS Support Power BI Blog (jpbap-sqlbi.github.io)](https://jpbap-sqlbi.github.io/blog/powerbi/aad_guestuser/)

### Data Activator
Data Activator データアラート では、受信者は Fabric テナントを所有する組織に属している必要があります。 
外部メール アドレスまたはゲスト メール アドレスのいずれにもメール アラートを送信はできません。

> [!NOTE]
> 参考情報：[Data Activator の制限事項 - Microsoft Fabric | Microsoft Learn ](https://learn.microsoft.com/ja-jp/fabric/data-activator/data-activator-limitations#allowed-recipients-of-email-alerts)

---
## 通知タイミングおよびトリガーできるデータ型と条件

### Power BI データアラート
Power BI データアラートでは、追跡対象データがユーザー設定のしきい値に達した場合、以下の条件を満たした場合にアラートが送信されます。
 
- 最後のアラートが送信されてから 1 時間以上または 24 時間以上 (選択したオプションによる) 経過していること
- データがしきい値を超えるまたは下回る場合
 
なお、対象の値は数値である必要があります。

### Data Activator
Data Activator データアラートでは、条件が満たされるたびにアラートがトリガーされます。

> [!NOTE]
> 参考情報：[Power BI から Data Activator のデータを取得する - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/data-activator/data-activator-get-data-power-bi#create-your-data-activator-trigger)


こちらも同様に対象の値は数値である必要があります。

また、メール、Teams、Power Automateのトリガーアクションによって制限があるため、ご注意ください。

 > [!NOTE]
> 参考情報：[Data Activator の制限事項 - Microsoft Fabric | Microsoft Learn ](https://learn.microsoft.com/ja-jp/fabric/data-activator/data-activator-limitations#maximum-number-of-trigger-actions)
 



トリガーの条件については、時間内での平均や回数、値の範囲など多様な条件を設定いただくことが可能です。


 > [!NOTE]
> 参考情報：[Data Activator の検出条件 - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/data-activator/data-activator-detection-conditions)
 



---
## 作成方法および管理方法

### Power BI データアラート

Power BI データアラート では、ダッシュボードのタイルの三点リーダー（ … ）を選択し、 [ アラートの管理 ] を選択して条件を設定します。
ビジュアルはゲージ、KPI、またはカード以外では[ アラートの管理 ]メニューが表示されませんのでご注意ください。

 <div align="center">
<img src="pbi_alert_creation_1.png">
</div>

作成したアラートの管理方法は、ダッシュボードのタイル自体、Power BI の [ 設定 ] メニュー、モバイル アプリの個別のタイルなどから管理が可能です。

 <div align="center">
<img src="pbi_alert_creation_2.png">
</div>

 > [!NOTE]
> 参考情報：[Power BI サービス ダッシュボードでデータ アラートを設定するためのチュートリアル。 - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/consumer/end-user-alerts)
> 参考情報：[Power BI サービスでデータ アラートを設定する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/create-reports/service-set-data-alerts#set-data-alerts-in-the-power-bi-service)
> 参考情報：[Power BI モバイル アプリでデータ アラートを設定する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/consumer/mobile/mobile-set-data-alerts-in-the-mobile-apps)
 
 
 

### Data Activator
Data Activator データアラート では、レポート内のビジュアルの三点リーダー(…)を選択し、[アラートの設定]を選択して条件を設定します。


 <div align="center">
<img src="data_activator_alert_creation_1.png">
</div>

作成したアラートの設定は、Reflex アイテムとして作成されます。
Power BI Service (Microsoft Fabric) の画面左下部にあるメニューから [Data Activator] を選択し、対象ワークスペースにアクセスすると、Reflex アイテムが表示され、設定の変更や削除を行うことが可能です。

 <div align="center">
<img src="data_activator_alert_creation_2.png">
</div>


 <div align="center">
<img src="data_activator_alert_creation_3.png">
</div>

 > [!NOTE]
> 参考情報：[Power BI から Data Activator のデータを取得する - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/data-activator/data-activator-get-data-power-bi#create-a-data-activator-trigger-from-a-power-bi-visual)

 
---
## おわりに
この記事では、Power BI と Data Activator のデータアラート機能の違いと利点について解説しました。Power BI のアラート機能は、シンプルで使いやすく、メールや Power Automateとの連携で Teams への通知が可能です。一方、Data Activator は複雑な条件設定や多様なビジュアルに対応し、より高度なデータ監視と通知を提供します。</br>
アラートを使用することで、データの変化にいち早く気づくことができ、迅速な意思決定、プロアクティブな対応を行うことが可能になります。
 

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)