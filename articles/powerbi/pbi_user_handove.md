---
title: Power BIユーザーの退職・異動への備え
date: 2024-03-29 00:00:00 
tags:
  - Power BI
  - 引き継ぎ
  - ロール
---
こんにちは、Power BI サポート チームの呂です。

Power BI でコンテンツを作成または共有しているユーザーが退職や異動になった場合、そのユーザーが保持していたコンテンツや権限の扱いについての質問がよく寄せられます。
本記事では、組織内の Power BI ユーザーの退職や異動が発生した場合に、コンテンツや権限を引き継ぐ方法についてご説明します。

<!-- more -->
> [!IMPORTANT]  
> 本記事編集時点と実際の機能に相違がある場合がございます。予めご了承ください。
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
## 目次
---
- [ユーザー削除後の動作について](#ユーザー削除後の動作について)
- [ユーザーロールの引き継ぎ](#ユーザーロールの引き継ぎ)
  - [Fabric管理者](#Fabric管理者)
  - [容量管理者と共同作成者](#容量管理者と共同作成者)
  - [データゲートウェイやデータソースロール](#データゲートウェイやデータソースロール)
  - [ワークスペースロール](#ワークスペースロール)
  - [セマンティックモデルやデータフローの所有者](#セマンティックモデルやデータフローの所有者)
- [役に立つREST API](#役に立つREST-API)

</br>

---
## ユーザー削除後の動作について
---
ユーザーアカウントが削除されると、アカウントは 30 日間中断状態になり、30 日の期間が経過すると完全削除されます。
ユーザーアカウントが完全削除されても、コンテンツ自体は削除されませんので、ご安心ください。
また、ユーザーが完全削除されると、Power BI で設定された権限も削除されます。
> [!TIP]
[組織からユーザーを削除する - Microsoft 365 admin | Microsoft Learn](https://learn.microsoft.com/ja-jp/microsoft-365/admin/add-users/delete-a-user?view=o365-worldwide)
[最近削除されたユーザーの復元または完全削除 - Microsoft Entra | Microsoft Learn](https://learn.microsoft.com/ja-jp/entra/fundamentals/users-restore)

なお、削除されたユーザーのマイワークスペースは [削除済み] として表示され、コンテンツは 90 日間保持されます。
Power BI管理者がユーザーのマイワークスペースにアクセスする機能を使用することで、マイワークスペースのガバナンスを実現可能です。
> [!TIP]
[Power BIワークスペースのガバナンス | Japan CSS Support Power BI Blog (jpbap-sqlbi.github.io)](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_workspace_governance/)
[Announcing My workspace governance improvement (Public Preview) | Microsoft Power BI Blog | Microsoft Power BI](https://powerbi.microsoft.com/en-us/blog/announcing-my-workspace-governance-improvement-public-preview/)


---
## ユーザーロールの引き継ぎ
---
退職や異動するユーザーがテナント、容量やワークスペースなどのロールを次の担当者に引き継ぎたい場合があるかと思います。
続いては、各ロールの引き継ぎ方法についてそれぞれ説明します。
</br>

---
### Fabric管理者
---
Fabric管理者は、Microsoft Fabric と Power BI 内でグローバル アクセス許可を持ち、サポート チケットを管理し、サービス正常性を監視できるテナントレベルの管理者ロールです。
Fabric管理者ロールは、特権ロール管理者またはグローバル管理者がMicrosoft 365 管理センターもしくはAzure Entraから変更できます。

Microsoft 365 管理センター：
![](1.png)

Azure Entra ：
![](2.png)

> [!TIP]
[Microsoft 365 管理センターを管理者ロールに割り当てる - Microsoft 365 admin | Microsoft Learn](https://learn.microsoft.com/ja-jp/microsoft-365/admin/add-users/assign-admin-roles?view=o365-worldwide)
[ユーザーに Microsoft Entra ロールを割り当てる - Microsoft Entra ID | Microsoft Learn](https://learn.microsoft.com/ja-JP/entra/identity/role-based-access-control/manage-roles-portal)
<br>

---
### 容量管理者と共同作成者
---
容量管理者は、容量にワークスペースを割り当てる、容量に対するユーザーアクセス許可を管理する、容量のワークロードを制御できるロールであり、容量共同作成者は、ワークスペースを容量に割り当てることができるロールです。
グローバル管理者、Fabric管理者、または容量管理者は、[管理ポータル]>[容量の設定]から Premium 容量の管理者と共同作成者を変更できます。
![](3.png)

FabricやEmbedded の場合、容量管理者はAzure portal 内で定義します。
![](4.png)

> [!TIP]
[Power BI Embedded の分析の容量と SKU - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/developer/embedded/embedded-capacity)
[Microsoft Power BI Premium 容量を管理する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-premium-capacity-manage)
<br>

---
### データゲートウェイやデータソースロール
---
グローバル管理者及び Fabric 管理者は、Power BI サービスの[設定]>[接続とゲートウェイの管理]、もしくは Power Platform 管理センターの[データ]画面からテナントにあるすべてのゲートウェイに対してロールを変更できます。
ゲートウェイ管理者は、管理者権限を持つゲートウェイに対してロールを変更できます。
![](5.png)

> [!TIP]
[オンプレミスデータゲートウェイのセキュリティーロール | Japan CSS Support Power BI Blog (jpbap-sqlbi.github.io)](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_gateway_role/)
[オンプレミス データ ゲートウェイの管理 | Microsoft Learn](https://learn.microsoft.com/ja-jp/data-integration/gateway/service-gateway-manage)
<br>

---
### ワークスペースロール
---
ワークスペース管理者は、ワークスペース画面の[アクセスの管理]からワークスペースロールを変更できます。
![](6.png)

ワークスペース管理者が削除されましても、Fabric 管理者は管理ポータルよりワークスペースのアクセス許可を変更できます。
![](7.png)

> [!TIP]
[Power BI のワークスペースのロール - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/collaborate-share/service-roles-new-workspaces)
[ワークスペースの管理 - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/admin/portal-workspaces)
<br>

---
### セマンティックモデルやデータフローの所有者
---
所有者はセマンティックモデルやデータフローに対するすべてのアクセス許可を持つロールです。
ワークスペースの共同作成者以上のロールを持つユーザーは、セマンティックモデルまたはデータフローの[設定]画面から[引き継ぎ]を選択することで、所有者を変更できます。
![](8.png)

> [!TIP]
[セマンティック モデルのアクセス許可 - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/connect-data/service-datasets-permissions)
[ワデータフローの構成と使用 - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/transform-model/dataflows/dataflows-configure-consume)
<br>

---
## 役に立つREST API
---
以下の REST API を使用することで、ユーザーがアクセスできる Power BI アイテム一覧をご確認いただけます。
[Admin - Users GetUserArtifactAccessAsAdmin - REST API (Power BI Power BI REST APIs) | Microsoft Learn](https://learn.microsoft.com/ja-jp/rest/api/power-bi/admin/users-get-user-artifact-access-as-admin)



以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。
<br>

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)