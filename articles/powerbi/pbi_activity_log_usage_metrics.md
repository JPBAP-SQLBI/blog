
---
title: Power BI のユーザーアクティビティ追跡方法の比較
date: 2023-12-29 14:00:00 
tags:
  - Power BI　　
  - Audit Log
  - Activity Log
  - Usage Metrics
  - 監査ログ
  - アクティビティログ
  - 利用状況メトリック
  - 使用状況メトリック
  - Admin Monitoring
  - 管理者監視ワークスペース
---


こんにちは、Power BI サポート チームのチャンです。   

Power BI のユーザーアクティビティの確認方法について、例えばどれぐらいの回数や頻度でレポートを閲覧しているか、実際ファイルのエクスポートを行なったかなどの行動に対して、ログを出力したり、レポート上で確認したいというご要望を、よくお問い合わせいただきますが、本ブログでは各追跡方法について詳しくご紹介いたします。

<!-- more -->


> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、　　
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
## 更新履歴
---
<span style="color: red;">
Update: 2023/12/29
</span>

Admin Monitoring ワークスペースの機能紹介を追加いたしました。
- [Admin Monitoring for Tenant Admins | Microsoft Power BI ブログ](https://powerbi.microsoft.com/ja-jp/blog/announcing-the-new-admin-monitoring-workspace-for-tenant-admins-public-preview/)


---
## Power BIアクティビティログ 
---

Power BI内のユーザーアクティビティを追跡する方法は、主に3つございます。

1. [利用状況メトリック](#利用状況メトリック)
2. [ActivityEvents](#ActivityEvents)
3. [監査ログ](#監査ログ)
4. [管理者監視ワークスペース（Admin Monitoring）](#管理者監視ワークスペース（admin-monitoring）)

以下にてそれぞれご紹介いたします。

---
## 利用状況メトリック
---

利用状況メトリックでは、各レポートの閲覧回数やパフォーマンス状況、よく使うレポートやレポートページ、よくアクセスしているユーザーの集計を簡単に可視化した機能をご利用いただけます。


#### ■前提条件

本機能を利用いただくための前提条件は以下となります。
- Power BI Pro または Premium Per User (PPU) のライセンスが必要です。
- レポート用の強化された利用状況の指標にアクセスするには、そのレポートに対する編集アクセス権を持っている必要があります。
- Power BI 管理者が、コンテンツ作成者に向けて[利用状況の指標を有効にしている](https://learn.microsoft.com/ja-jp/power-bi/admin/service-admin-portal-audit-usage)必要があります。

#### ■利用手順
有効化する手順について、以下ご案内いたします。

1. ワークスペースのコンテンツ リストのいずれかから、レポートのオプション メニューを開き、 [利用状況のメトリック レポートを表示] を選択します。 
<div align="center">
<img src="usage_metrics1.png" alt="利用状況メトリック レポートを表示" title="利用状況メトリック レポートを表示">
</div>

2. メトリックレポートが生成中の間は、以下のようなポップアップウィンドウが表示されます。
<div align="center">
<img src="usage_metrics2.png" alt="メトリックレポート作成中" title="メトリックレポート作成中">
</div>

3. レポートの生成が完了したら、 [使用状況メトリックの表示] を選択します。
<div align="center">
<img src="usage_metrics3.png" alt="使用状況メトリックの表示" title="使用状況メトリックの表示">
</div>

4. 初めて実行する場合は、古い利用状況の指標に関するレポートが開かれる場合があります。 強化された利用状況の指標に関するレポートを表示するには、右上の [新しい使用状況レポートをオフにする] スイッチを [オン] に切り替えます。
※強化された新しい利用状況では、古い利用状況より、多くの情報を可視化されています。例えば、同じワークスペース内の各レポートの閲覧状況の比較や、トレンドやパフォーマンスをご確認いただけます。
<div align="center">
<img src="usage_metrics4.png" alt="新しい使用状況レポートをオンにする" title="新しい使用状況レポートをオンにする">
</div>


> **参考情報：**
> - [新しいモダン ワークスペースで使用状況メトリックを監視する (プレビュー) - Power BI | Microsoft Docs](https://learn.microsoft.com/ja-jp/power-bi/collaborate-share/service-modern-usage-metrics)


---
## ActivityEvents
---

PowerShell を使ってユーザーアクティビティのログを出力できる機能ですが、Power BI サービス上の操作画面はございません。


#### ■前提条件
- Power BI (Fabric) 管理者、またはグローバル管理者のアカウントでサインインしていること
- PowerShellでモジュールのインストール

```CMD
Install-Module -Name MicrosoftPowerBIMgmt

```

 
#### ■利用手順

PowerShellでGet-PowerBIActivityEventを使用します。
一回で取得できるのは1日分なので、開始日と終了日で同じ日付値を参照する必要があります。

```CMD
Login-PowerBI

$activities = Get-PowerBIActivityEvent -StartDateTime '2022-07-25T00:00:00' -EndDateTime '2022-07-25T23:59:59' | ConvertFrom-Json

$activities

# エクスポートするファイルのパスを指定
$outputFile = "C:\Temp\activities.csv"
$activities | Export-Csv $outputFile -NoTypeInformation

```
#### ■PowerShellの実行結果

<div align="center">
<img src="powershellactivities2.png" alt="PowerShellの実行結果" title="PowerShellの実行結果">
</div>

#### ■エクスポートされたcsvファイル

<div align="center">
<img src="powershellactivities.png" alt="エクスポートされたcsvファイル" title="エクスポートされたcsvファイル">
</div>



> **参考情報：**
> - [アクティビティ ログの使用 - Power BI | Microsoft Docs](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-admin-auditing#use-the-activity-log)

---
## 監査ログ
---

監査ログは、Power BI独有の機能ではなく、Microsoft 365のコンプライアンス管理センターの機能でございます。
そのため、一度有効にすると、Power BIのログだけでなく、すべてのMicrosoft 365製品における監査ログが記録されるようになります。

#### ■前提条件
- 監査ログにアクセスするには、グローバル管理者であるか、Exchange Online で Audit Logs (監査ログ) または View-Only Audit Logs (表示専用監査ログ) ロールが割り当てられている必要があります。

#### ■利用手順

1. Power BIサービスへサインインし、[設定]>[管理ポータル] へアクセスします。
<div align="center">
<img src="auditlog1.png" alt="管理ポータルへアクセス" title="管理ポータルへアクセス">
</div>

2. [監査ログ] > [Microsoft 365 管理センターに移動]を選択します。
<div align="center">
<img src="auditlog2.png" alt="Microsoft 365コンプライアンス管理センター" title="Microsoft 365コンプライアンス管理センター">
</div>

3. 開始日と終了日を選択し、アクティビティで、Power BIで絞り、必要なイベントのみ選択します。
※もし監査ログが有効化されていない場合、有効化ボタンをクリックする必要がございます。
<div align="center">
<img src="auditlog3.png" alt="監査ログの検索" title="監査ログの検索">
</div>

> **参考情報：**
> - [監査ログの使用 - Power BI | Microsoft Docs](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-admin-auditing#use-the-audit-log)


---
## 管理者監視ワークスペース（Admin Monitoring）
---

2023年5月から新規に公開された管理者監視ワークスペース（Admin Monitoring）という機能では、「Feature Usage and Adoption」 と 「Purview Hub」 の二つのレポートが用意されています。

「Feature Usage and Adoption」の方は、監査ログに基づいて構築された分析ビューが用意されており、誰が何をしているかを理解するのに役立ち、特定の傾向、パターン、アクティビティを特定することで Power BI をより適切に管理できます。

<div align="center">
<img src="https://powerbiblogscdn.azureedge.net/wp-content/uploads/2023/05/Picture1.png">
</div>

<br>
「Purview Hub」の方は、機密データと項目の承認に関する分析情報を提供するレポートが含まれており、データ カタログ、情報保護、データ損失防止、監査など、Microsoft Purview ガバナンスおよびコンプライアンス ポータルのより高度な機能へのリンクとしても機能します。

<div align="center">
<img src="https://learn.microsoft.com/ja-jp/fabric/governance/media/use-microsoft-purview-hub/microsoft-purview-hub-full-report-admin.png">
</div>

#### ■前提条件
- Power BI (Fabric) 管理者、またはグローバル管理者のアカウントでサインインしている必要があります。
- ワークスペース内のレポートを閲覧するには、 Power BI Pro または Premium Per User (PPU) のライセンスが必要です。

#### ■利用手順

1. 管理者アカウントにて、[Power BIサービス](https://app.powerbi.com/)へサインインし、[ワークスペース] > [Admin monitoring] の順で選択します。
<div align="center">
<img src="admin_monitoring1.png">
</div>

2. ワークスペース内に、自動的に「Feature Usage and Adoption」と「Purview Hub」という二つのレポート及びセマンティックモデル（データセット）が生成されています。
<div align="center">
<img src="admin_monitoring2.png">
</div>

> **参考情報：**
> - [管理者監視ワークスペースとは? - Microsoft Fabric | Microsoft Docs](https://learn.microsoft.com/ja-jp/fabric/admin/monitoring-workspace)
> - [機能の使用状況と導入レポート - Microsoft Fabric | Microsoft Docs](https://learn.microsoft.com/ja-jp/fabric/admin/feature-usage-adoption)
> - [Admin Monitoring for Tenant Admins | Microsoft Power BI ブログ](https://powerbi.microsoft.com/ja-jp/blog/announcing-the-new-admin-monitoring-workspace-for-tenant-admins-public-preview/)
> - [Microsoft Fabric の Microsoft Purview ハブ (プレビュー)- Microsoft Fabric | Microsoft Docs](https://learn.microsoft.com/ja-jp/fabric/governance/use-microsoft-purview-hub?tabs=admin-view)


---
## 比較
---

以下にて各追跡方法について表にまとめました。

|       | **監査ログ**  | **PowerShell ActivityEvents**  | **利用状況メトリックレポート**  |  **Admin Monitoring** | 
| -------- | -------- | -------- | -------- | -------- | 
| **目的** | Power BI およびその他サービスのユーザーアクティビティの追跡   | Power BI ユーザー アクティビティの追跡 | Power BIのレポートの利用状況確認（ワークスペース単位） |  Fabric（ Power BI 含め）の各機能の利用状況確認（テナント単位） | 
| **取得項目範囲**    | Power BI 監査イベントに加えて、SharePoint Online、Exchange Online、Dynamics 365、及びその他のサービスからのイベントが含まれます | Power BI 監査イベントのみ  | Power BI のワークスペース上のレポートの閲覧状況のみ | Fabric（ Power BI 含め）テナント内の機能の利用状況のみ   | 
| **必要な権限**   | ・ View-Only Audit Logs (表示専用監査ログ)<br>・グローバル管理者<br>・監査人    | ・グローバル管理者<br>・Power Platform 管理者<br>・Power BI (Fabric) 管理者  | ワークスペースの管理者・メンバー・共同作成者      |・グローバル管理者<br>・Power BI (Fabric) 管理者  | 
| **必要なPower BIライセンス** |  -  | -   - | Power BI Pro または Premium Per User (PPU) のライセンス | Power BI Pro または Premium Per User (PPU) のライセンス | 
| **保管期間**   | 90日間 / 180日間※ | 30日間（一度に1日分のみ取得可能）| 30日間 | 30日間  | 
| **タイムラグ** | 監査を有効にしてから監査データを表示できるようになるまで、最大で 48 時間の遅延が発生する場合があります。                        | Power BI イベントを取得するまでに、最大 30 分の遅延が発生することがあります。 | 新しい利用状況データをインポートするには、最大で 24 時間かかることがあります。 | 1 日 1 回、自動的に更新され、管理者ワークスペースに初めてアクセスしてから約 10 分後に更新が行われます。 | 
 

※　監査 (Standard) の既定の保持期間が 90 日から 180 日に変更されました。 2023 年 10 月 17 日より前に生成された監査 (Standard) ログは、90 日間保持されます。 2023 年 10 月 17 日以降に生成された監査 (Standard) ログは、新しい既定の保持期間の 180 日に従います。
また、Office 365 E5 または Microsoft 365 E5 ライセンスの場合、監査ログ180日間（最長1年間）を保持することができます。E5 ライセンスに加えて、10 年間の監査ログ保持のアドオン ライセンスもございます。

> 参考情報：
> - [監査ログの保持ポリシーを管理する](https://learn.microsoft.com/ja-jp/microsoft-365/compliance/audit-log-retention-policies?view=o365-worldwide)


</br>


以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)