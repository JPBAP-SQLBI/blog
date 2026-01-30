---
title: Power BI の管理者ロールについて
date: 2026-01-30 00:00:00 
tags:
  - Power BI
  - Power BI サービス
  - Admin
---

こんにちは、Power BI サポート チームの中川です。

Power BI / Microsoft Fabric には複数の管理者ロールが存在しますが、公式ドキュメントはロールや機能単位で分散しており、「どのロールで、どこまで管理できるのか」を横断的に把握することが難しい場合があります。 
その結果、次のような課題が発生することが想定されます。 
・管理者ロールを付与したにも関わらず、想定していた操作が実行できない 
・本来は不要な高権限ロールが広範に付与されている 
・管理者ロールごとの責務が整理されないまま運用が開始されている 

本ブログでは、こうした背景を踏まえ、Power BI / Microsoft Fabric における代表的な管理者ロールそれぞれの管理対象を整理してご紹介いたします。 



<!-- more -->
> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
## 目次
---
* [管理者ロールの全体像](#管理者ロールの全体像)
* [Fabric 管理者](#Fabric-管理者)
* [容量管理者](#容量管理者)
* [ワークスペース管理者](#ワークスペース管理者)
* [データゲートウェイ管理者 ](#データゲートウェイ管理者)
* [おわりに](#おわりに)


---
## 管理者ロールの全体像 
---
Power BI / Microsoft Fabric の管理者ロールは、主に以下のロールがあります。 

これらのロールは上下関係ではなく、管理対象ごとに責務が分かれています。 
次章からは、それぞれのロールについて詳しく見ていきます。 

| ロール名                   | 管理範囲          | 主な権限                                      |
|----------------------------|-------------------|-----------------------------------------------|
| Fabric 管理者              | テナント全体      | Fabric ポータルのテナント設定やその他の設定の管理 |
| 容量管理者                 | Premium 容量 / Fabric 容量 | 容量設定やワークスペースへの割り当て、パフォーマンス監視        |
| ワークスペース管理者        | ワークスペース    | ワークスペースの設定とアクセスの管理           |
| データゲートウェイ管理者    | オンプレミスデータゲートウェイ </br>VNet データ ゲートウェイ  | ゲートウェイ構成、資格情報、ユーザーの割り当ての管理  |

>[!NOTE]
> 参考情報：[Microsoft Fabric 導入ロードマップ: システム監視 - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/guidance/fabric-adoption-roadmap-system-oversight#roles-and-responsibilities)


---
## Fabric 管理者
---
Fabric 管理者は、Power BI を含むMicrosoft Fabricテナント全体を管理するロールです。グローバル管理者および Power Platform 管理者も、Fabric 管理者と同等の操作が可能です。 
Fabric 管理者は、組織全体のガバナンスやセキュリティ設定などを担うロールであり、多くのタスクを実行することが可能です。 

主に以下のような重要な管理タスクを担当します。 
- テナント設定の管理（有効化/無効化、ユーザー制御） 
- テナント全体のワークスペースの管理
- 監査ログ・アクティビティログ
- 上記以外の管理ポータルで実行できる機能 

### テナント設定の管理 
管理ポータルの「テナント設定」では、Power BI / Fabric の機能を組織単位で制御できます。 
- 新機能や特定機能の有効化／無効化 
- 外部共有、エクスポートなどの情報漏えいリスク制御 
- セキュリティグループ単位での許可設定 

これらの設定は、個々の利用者やワークスペース管理者が変更できるものではなく、組織としてのガバナンス方針を反映するための設定です。そのため、テナント設定の管理は Fabric 管理者の中でも特に重要なタスクに位置づけられます。 

>[!NOTE]
> 参考情報：
>[Power BI 実装計画: テナント管理 - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/guidance/powerbi-implementation-planning-tenant-administration#govern-tenant-settings) 
>[テナント設定について - Microsoft Fabric | Microsoft Learn ](https://learn.microsoft.com/ja-jp/fabric/admin/about-tenant-settings)
>[テナント設定のインデックス - Microsoft Fabric | Microsoft Learn ](https://learn.microsoft.com/ja-jp/fabric/admin/tenant-settings-index)
>[Power BI 利用時に考慮すべき主要なセキュリティ設定](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_security_settings/)


### ワークスペースの管理 
管理ポータルの「ワークスペース」から、ワークスペースの管理者でない場合でも管理権限の取得や操作が可能です。 
例として、以下のような状況において Fabric 管理者が介入することが想定されます。 

- ワークスペース管理者が不在となっている場合 
- 意図せず削除されたワークスペースの復元が必要な場合 
- 何らかの理由でワークスペースへのアクセスが必要な場合 


なお、ワークスペースの管理者権限の取得は通常運用で頻繁に行うものではなく、上記の例外的な状況で利用されることを前提に運用いただくことを推奨します。 
以下に、共有ワークスペースおよび個人用それぞれで行える操作について説明します。 

#### 共有ワークスペースの管理 
ライセンスモードの変更や復元など、運用上の重要な操作を実行できます。 
- アクセス権の取得：ワークスペースのアクセス権がない場合でも、ワークスペースのアクセス権を追加・削除することが可能
- 名前変更やライセンスモードの変更：ワークスペースに設定されている名称やライセンスモードを変更可能
- ワークスペースの復元：削除済みワークスペースを一定期間内で復元可能
（期間については[こちらの公開情報](https://learn.microsoft.com/ja-jp/fabric/admin/portal-workspaces#workspace-retention)をご参照） 

>[!NOTE]
> 参考情報：[ワークスペースを管理する - Microsoft Fabric | Microsoft Learn ](https://learn.microsoft.com/ja-jp/power-bi/guidance/powerbi-implementation-planning-tenant-administration#govern-workspaces)

#### 個人用ワークスペースの管理 
マイワークスペースに対して既定の容量を指定することや一時的なアクセス権を取得し、容量の統制や復元を行うことができます。 
- 一時的なアクセス権の取得：他ユーザーのマイワークスペースへ24時間のアクセス権を取得しアクセス可能です
- 対象ワークスペースの[詳細]からIDを取得し、以下URLにてアクセスです
  https://app.powerbi.com/groups/[ワークスペースID] 
- 既定の容量の指定：特定の容量をマイ ワークスペースの既定の容量として指定できます 
- 復元：削除された マイ ワークスペースをアプリ ワークスペースとして復元可能 

 
>[!NOTE]
> 参考情報：[ワークスペースを管理する - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/admin/portal-workspaces#designate-a-default-capacity-for-my-workspaces)

 

### テナント全体の監査ログ取得 
Fabric 管理者は、Microsoft Purview コンプライアンス ポータルを通じて、Power BI および Fabric のアクティビティログを取得し、いつ・誰が・どのような操作を行ったかを把握できます。 
機能についての詳細や使用方法につきましては、以下のブログをご参照ください。 

>[!NOTE]
> 参考情報：[Power BI のユーザーアクティビティ追跡方法の比較 | Japan CSS Support Power BI Blog](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_activity_log_usage_metrics/#%E7%9B%A3%E6%9F%BB%E3%83%AD%E3%82%B0)

---
## 容量管理者 
---
容量管理者は、Power BI Premium 容量、Microsoft Fabric 容量、Embedded 容量、Fabric 試用版容量の管理を担当するロールです。 
本章では、このうち Power BI Premium 容量 および Microsoft Fabric 容量 に焦点を当てて解説します。 

 
### 容量の構成と監視 

ご利用中の容量については、処理速度の低下を防ぐために、上位の SKU へのアップグレードや、自動的にコンピューティング容量を追加する自動スケーリングの設定が可能です。 

- Premium 容量：管理ポータルからサイズ変更や自動スケーリング設定が可能 
- Fabric 容量：Azure Portal からサイズ変更が可能（自動スケーリングは非対応） 

<div align="center">
<img src="SKU_size_change.png">
<figcaption>左：Power BI Premium 容量　　右：Microsoft Fabric 容量 </figcaption>
</div>

>[!NOTE]
> 参考情報：[Fabric 容量を管理する - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/admin/capacity-settings?tabs=power-bi-premium#manage-your-capacity)

### ワークスペースへの容量の割り当て
ワークスペースで利用するライセンスモードに容量を割り当てることができます。 

なお、容量の設定画面から共同作成者のアクセス許可を付与することで、そのユーザーもワークスペースに容量に割り当てることが可能になります。 

<div align="left">
<img src="Capacity_contributor_permissions.png">
</div>

### 容量のパフォーマンス監視 
Microsoft Fabric Capacity Metrics アプリを使用して、容量全体の CU（Capacity Unit）消費状況を監視します。 
これにより、「容量が継続的に高負荷となっていないか」、「特定のワークロードやワークスペースに負荷が集中していないか」、「スケールアップや最適化が必要かどうか」のような運用判断を行います。 

Microsoft Fabric Capacity Metrics アプリのインストールには容量管理者権限が必要ですが、作成されたワークスペースに対して閲覧者ロールを付与することで、他のユーザーもレポートを参照できます。 

<div align="left">
<img src="Microsoft_Fabric_Capacity_Metrics_App.png">
</div>

>[!NOTE]
> 参考情報：[Microsoft Fabric Capacity Metrics アプリの見方 | Japan CSS Support Power BI Blog ](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_capacity_metrics/)

### ワークロード設定の構成
容量上で実行される Power BI ワークロードの設定を構成でき、セマンティック モデルやデータフローなどの容量リソースの消費傾向や運用方針に応じたチューニングを行うことができます。 


 <div align="left">
<img src="PBI_Workload.png">
</div>

>[!NOTE]
> 参考情報：[Power BI Premium でワークロードを構成する方法 - Microsoft Fabric | Microsoft Learn ](https://learn.microsoft.com/ja-jp/fabric/enterprise/powerbi/service-admin-premium-workloads)


### 委任されたテナントの設定 
通常、テナント設定は Fabric 管理者のみが制御可能ですが、委任されたテナント設定を利用することで、特定の設定に限り、容量管理者が容量単位で制御できるようになります。 
例えば、テナント全体では「ユーザーは Fabric アイテムを作成できます」を有効化しているが、特定の容量だけはその設定をオーバーライドし無効化する、のような設定が可能です。 

 
<div align="center">
<img src="Delegate_tenant_settings.png">
<figcaption>左：テナント設定　　右：容量設定内の委任されたテナント設定</figcaption>
</div>
 
その他にも、容量管理者はサージ保護（容量の過負荷を防ぐための設定）、マイワークスペースの優先容量を設定する項目などがあります。詳細については、容量の設定 の項目を参照してください。 


---
## ワークスペース管理者 
---
ワークスペース管理者は、特定のワークスペース単位で管理責任を持つロールです。コンテンツの作成や利用はもちろん可能ですが、他のロールに付与されない権限を含め、ワークスペース全体の運用状態に対して最終的な責任を負うロールです。 
 
Microsoft Fabric と Power BI は同一のワークスペース上に共存しますが、付与されているロールによって実行可能な操作が異なります。詳細な権限の違いについては、以下の公式ドキュメントをご参照ください。 

 
>[!NOTE]
> 参考情報：
>[Power BI のワークスペースのロール - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/collaborate-share/service-roles-new-workspaces)
>[Microsoft Fabric のワークスペースのロール - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/fundamentals/roles-workspaces#microsoft-fabric-workspace-roles)


---
## データゲートウェイ管理者
---
データゲートウェイ管理者は、Power BI および Microsoft Fabric からオンプレミスや仮想ネットワーク内のデータソースへ安全に接続するための「データゲートウェイ」を管理するロールです。 
対象となるゲートウェイには、以下の 2 種類が含まれます。 

<b>オンプレミス データゲートウェイ</b></br>
社内ネットワークやオンプレミス環境上のデータソースに接続するために使用され、サーバーや VM 上にインストールして運用します。 

<b>VNet データゲートウェイ</b></br>
Azure の仮想ネットワーク内で管理され、Azure PaaS サービスや VNet 内リソースへの接続を主な用途とします。Microsoft 管理型サービスであり、ハードウェア管理は不要です。 


データゲートウェイ管理者は、以下のような管理タスクを担当します。 
- ゲートウェイの管理者およびユーザーの追加・削除 
- 接続 (データ ソース)および資格情報の管理 
- ゲートウェイの稼働状況や負荷の監視、トラブルシューティング 

ゲートウェイ管理者のロールの詳細につきましては、以下のブログをご参照ください。 

[オンプレミスデータゲートウェイのセキュリティーロール | Japan CSS Support Power BI Blog ](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_gateway_role/)

 


---
## おわりに
本ブログでは、Power BI / Microsoft Fabric における主要な管理者ロールについて、管理対象・責務・役割分担の観点から整理しました。 
誰が・どの範囲に・どの責任を持つのかを明確にし、管理者ロールの棚卸しや運用設計を見直す際の判断材料として、本ブログが少しでも皆様のお役に立てますと幸いでございます。 


---
**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)