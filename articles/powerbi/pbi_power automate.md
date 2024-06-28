---
title: Power BI とData Activator のデータアラート機能の比較
date: 2024-06-28 00:00:00 
tags:
  - Power BI サービス
  - Data Activator
  - データアラート
  - Fabric
---

こんにちは、Power BI サポート チームの中川です。

Power BI では、Power Automate と連携することで、Power BI だけでは実現が難しい自動化プロセスを作成できます。例えば、任意のタイミングでセマンティックモデルを更新する、レポートを定期的にPDFに変換してメール送信するなど、多岐にわたる自動化シナリオが実現可能です。

本ブログでは、Power BI と Power Automate の連携について効果的な活用事例をご紹介します。


<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
## 目次
---
* [Power Automate とは](#Power-Automate-とは)
* [セマンティックモデルを任意のタイミングで更新する](#セマンティックモデルを任意のタイミングで更新する)
* [データフローとセマンティックモデルを順番に更新する](#データフローとセマンティックモデルを順番に更新する)
* [SharePoint の Excel ファイルが更新されたことをトリガーにセマンティックモデルを更新する](#SharePoint-の-Excel-ファイルが更新されたことをトリガーにセマンティックモデルを更新する)
* [データアラートの通知を Teams に送信する](#データアラートの通知を-Teams-に送信する)
* [レポートを定期的にエクスポートしてメール送信する](#レポートを定期的にエクスポートしてメール送信する)
* [[番外編] Power BI レポートに Power Automate のボタンを追加する](#[番外編]-Power-BI-レポートに-Power-Automate-のボタンを追加する)
* [おわりに](#おわりに)

---
## Power Automate とは
---
Power Automate はMicrosoft が提供するローコードの自動化ツールで、さまざまなアプリケーションやサービス間でワークフローを自動化することができます。これにより、手作業の手順を減らし、効率的かつ効果的な業務プロセスが実現可能となります。

なお、 Power Automate にはクラウドフロー (DPA)とデスクトップフロー (RPA)の2種類があります。本ブログでは、クラウドフロー(DPA)に焦点を当てて解説します。

>[!NOTE]
> 参考情報：[Microsoft Power Automate – Process Automation プラットフォーム | Microsoft](https://www.microsoft.com/ja-jp/power-platform/products/power-automate#tabs-pill-bar-ocb9d4_tab3)


以降の章では、具体的な活用シナリオや手順について説明します。



---
## セマンティックモデルを任意のタイミングで更新する
---

### 想定されるシナリオと課題
Power BI Service ではセマンティックモデルのスケジュール更新機能があり、月次や週次、30分間隔での設定が可能です。</br>
しかし、これらの設定以外のユースケース、例えば、何かをトリガーとしてセマンティックモデルを更新する、10分に1回セマンティックモデルを更新するなどの場合、標準機能では対応できません。


### 解決策
Power Automate を利用することで、より柔軟なスケジュール設定が可能になります。

// 手順ご参考
1. Power Automate でスケジュール済みクラウド フローを設定する。
2. 作成したフローにデータセットの更新アクションを追加する。

</br>
Power Automateから [スケジュール済みクラウドフロー]を選択します。 

<div align="center">
<img src="recurrence_semantic_model_refresh_1.png">
</div>

</br>
[Recurrence] にスケジュールを設定します。
<div align="center">
<img src="recurrence_semantic_model_refresh_2.png">
</div>

</br>
[データセットの更新] にワークスペースとデータセット（セマンティックモデル）を設定します。
こちらはプルダウンから選択することができます。
<div align="center">
<img src="recurrence_semantic_model_refresh_3.png">
</div>

</br>
なお、ライセンスによって自動更新の回数に制約がありますのでご注意ください。

- **Pro 容量**
  - 1日あたりの更新回数はセマンティックモデルあたり8回/日まで（スケジュールされた更新と Power Automate による更新の合計）。

- **Premium 容量（Per Capacity, Per User）**
  - Power Automate による更新には制限はありません。
  - Power BI Service でのスケジュール更新は48回/日まで可能です。

---
## データフローとセマンティックモデルを順番に更新する

### 想定されるシナリオと課題
データフローをデータソースとするレポートを作成する場合、Power BI Service にはデータフローとセマンティックモデルが存在することになります。</br>
しかしながら、データフローが更新されても、セマンティックモデルは自動的に更新されません。そのため、それぞれのスケジュール更新を設定をすることが考えられますが、タイミングにずれが生じたり、無駄な待ち時間が発生するなど、効率的ではない状況が発生します。


### 解決策

Power Automate を利用することで、データフローが更新されたことをトリガーに、セマンティックモデルの更新を行うことが可能です。

// 手順ご参考
1.	Power BI Serviceでデータフローの更新スケジュールを設定する
2.	Power Automate でデータフローの更新をトリガー、セマンティックモデルの更新する

具体的な作成方法については、以下のリンクをご参照ください。
> [!NOTE]
> 参考情報 ：[Power BI サービスのデータセット更新手順について | Japan CSS Support Power BI Blog (jpbap-sqlbi.github.io)](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_refresh_settings/)
> 参考情報 ：[データフローと Power BI セマンティック モデルを順番にトリガーする - Power Query | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-query/dataflows/trigger-dataflows-and-power-bi-dataset-sequentially?WT.mc_id=DP-MVP-5004418)

注意事項として、データフローが複数ある場合、例えば、データフロー1 -> データフロー2 -> セマンティックモデルの順で自動更新を行うシナリオでは、上記手順で自動化フローを作成することはできません。

そのため、代替手段として以下が考えられますので、ご検討いただけますと幸いです。

- 複数のデータフローのうち、最も遅く更新されるデータフローのスケジュールを最後に設定し、その更新完了をトリガーにしてセマンティックモデルの更新を行う方法。（ただし、各データフローの更新にかかる時間が異なる場合、この方法では必ずしも正確な更新タイミングを保証できない点に注意が必要です）
- APIを利用する方法
  1. APIでデータフローを更新する
  2. APIでデータフローの更新時間（refreshTime）を取得する
  3. すべてのデータフローの更新が確認できたら、セマンティックモデルの更新アクションを実行する

> [!NOTE]
> 参考情報 ：[Dataflows - Refresh Dataflow - REST API (Power BI Power BI REST APIs) | Microsoft Learn](https://learn.microsoft.com/ja-jp/rest/api/power-bi/dataflows/refresh-dataflow)
> 参考情報 ：[Dataflows - Get Dataflow - REST API (Power BI Power BI REST APIs) | Microsoft Learn](https://learn.microsoft.com/ja-jp/rest/api/power-bi/dataflows/get-dataflow)



---
## SharePoint の Excel ファイルが更新されたことをトリガーにセマンティックモデルを更新する

### 想定されるシナリオと課題
OneDrive for Business または SharePoint に格納されている、ユーザーが適宜編集する Excel ファイルを基に Power BI レポートを作成するシナリオでは、次のような課題が想定されます。

- ユーザーが Excel ファイルを編集するタイミングは不定期であるため、Power BI Service で手動でセマンティックモデルを更新する必要がある。
- 自動更新のスケジュールを設定しても、Excel の更新タイミングと合わない場合がある。
- [OneDrive または SharePoint Online からセマンティックモデルを更新する方法](https://learn.microsoft.com/ja-jp/power-bi/connect-data/refresh-desktop-file-onedrive) で自動更新はできるが、1時間に1回の更新だと少ない、更新タイミングが厳密には分からないなどの問題が生じる。


### 解決策
Power Automate を利用することで、Excel ファイルの更新を自動的に検知し、セマンティックモデルの更新を行うことが可能です。

// 手順ご参考
1. Power BI Desktop から OneDrive for Business または SharePoint の Excel ファイルに接続、Power BI Serviceにレポートを発行する
2. Power Automate を使用して、Excel ファイルの更新を自動的に検知し、セマンティックモデルの更新を自動的にトリガーするフローを作成する。

具体的な作成方法については、以下のリンクをご参照ください。

> [!NOTE]
> 参考情報 ：[Power BI Desktop で職場または学校向け OneDrive のリンクを使用する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/connect-data/desktop-use-onedrive-business-links)
> 参考情報 ：[SharePoint ファイルが更新されると Power BI データセットを更新する | Microsoft Power Automate](https://make.preview.powerautomate.com/environments/839eace6-59ab-4243-97ec-a5b8fcc104e4/galleries/public/templates/78375cfc773e45c1b9f87d14de7d7f37/)




---
## データアラートの通知を Teams に送信する

### 想定されるシナリオと課題
Power BI にはデータアラート機能があり、データが変化したときにユーザーに通知することが可能です。</br>
標準のデータアラート機能ではメール送信のみが可能であり、Microsoft Teams への送信はできません。これでは、チーム全体での迅速な情報共有や対応が難しくなります。

データアラート機能の詳細については、以下のリンクをご参照ください。
> [!NOTE]
> 参考情報 ：[Power BI サービスでデータ アラートを設定する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/create-reports/service-set-data-alerts)
> 参考情報 ：[Power BI とData Activator のデータアラート機能の比較 | Japan CSS Support Power BI Blog (jpbap-sqlbi.github.io)](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_data_activator_alert/)




### 解決策
Power Automate を利用することで、データアラートをトリガーにして Microsoft Teams に通知を自動送信することができます。

// 手順ご参考
1. Power Automate で Power BI のアラートがトリガーされたときに実行するアクションを作成する。
2. 作成したフローに Microsoft Teams への通知アクションを追加し、アラートの詳細を送信する。

具体的な作成方法については、以下のリンクをご参照ください。


> [!NOTE]
> 参考情報 ：[Power BI サービス ダッシュボードでデータ アラートを設定するためのチュートリアル。 - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/consumer/end-user-alerts)


---
## レポートを定期的にエクスポートしてメール送信する

### 想定されるシナリオと課題
Power BI レポートを定期的にエクスポートし配布するシナリオを想定します。</br>
エクスポートされたレポートを特定のユーザーに配布することは手動で行うと時間と手間がかかります。例えば、毎週の営業報告書や月次の財務報告書など、定期的に更新が必要なレポートでは、手動の作業が増え、効率が低下する可能性があります。


### 解決策
Power Automate を利用することで、レポートのエクスポートと配布を自動化することが可能です。

// 手順ご参考
1. Power Automate を使用してレポートをエクスポートするフローを作成する。Power BI レポートは、以下の3つの形式でエクスポートが可能です
   - PDF
   - PNG
   - PPTX
2. 作成したフローにメール送信アクションを追加し、エクスポートされたレポートを特定のユーザーに自動で送信する。

> [!NOTE]
> 参考情報 ：[Power Automate を使用してレポートをエクスポートしてメールで送信する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/collaborate-share/service-automate-power-bi-report-export)


---

## [番外編] Power BI レポートに Power Automate のボタンを追加する
これまで 、Power BI だけでは実現できなかったことが、Power Automate を組み合わせることで実現可能になるシナリオを紹介してきました。</br>
Power BI レポートには、 Power Automate のフローを実行するボタンを作成することも可能ですので、こちらについても紹介します。
例えば、Power BI レポート内にボタンを配置し、それをクリックすることで Excel にデータを追加したり、セマンティックモデルを更新したりといった操作を実行することができます。

> [!NOTE]
> 参考情報 ：[Power BI 用の Power Automate ビジュアルを作成する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/create-reports/power-bi-automate-visual?tabs=powerbi-desktop)

テンプレートがいくつかございますので、適宜検索してご利用の検討をお願いします。

> [!NOTE]
> 参考情報 ：[テンプレートの参照 | Microsoft Power Automate](https://make.preview.powerautomate.com/environments/839eace6-59ab-4243-97ec-a5b8fcc104e4/templates?culture=ja-jp&country=jp)

なお、テンプレートはPower BI Desktop、Power BI Service でフロー作成する画面で使用することが可能です。
<div align="center">
<img src="power-bi-automate-visual.png">
</div>

注意事項として、Power BI レポート内のボタンで実行するフローは、レポート内で直接作成する必要があります。Power Automate で事前に作成したフローは利用できません。</br>
また、その他にもいくつかの制限事項があります。詳細については、以下のリンクをご確認ください。

> [!NOTE]
> 参考情報 ：[Power BI 用の Power Automate ビジュアルを作成する - 考慮事項と制限事項 - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/create-reports/power-bi-automate-visual?tabs=powerbi-desktop#considerations-and-limitations)


---
## おわりに
この記事では、Power BI と Power Automate の連携によって実現できる自動化プロセスの活用事例について解説しました。

当チームは Power BI サポートチームのため、Power Automate 製品に関する専門的なサポートは提供しておりません。</br>
しかし、ご検証いただくうえで、セマンティックモデルが更新できないなどの Power BI に関するトラブルシューティング等の観点ではご案内することが可能ですので、Power BI 観点で問題がございましたら、お持ちの有償ライセンスやご契約のサポート範囲をご確認の上、お気兼ねなくお問い合わせください。


以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)