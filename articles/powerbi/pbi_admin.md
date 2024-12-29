---
title: Power BI の管理について 
date: 2024-10-31 00:00:00 
tags:
  - Power BI
  - Admin
  - 管理者
  - Power BI サービス
  - Power BI Service
---
こんにちは、Power BI サポート チームの呂です。 

Power BI は、ビジネス インテリジェンスとデータ分析のための強力なツールであり、組織内のデータ ドリブンな意思決定を支援します。その機能を最大限に活用し、データのセキュリティとガバナンスを確保するためには、Fabric 管理者の役割が非常に重要です。本記事では、Power BI の管理に関する主な機能を説明し、管理者が知っておくべきポイントを包括的に紹介します。 

<!-- more -->
> [!IMPORTANT]  
> 本ブログで紹介する機能に加え、他にも多くの管理者向け機能が存在し、また新しい機能が随時追加されています。
> 最新情報については、Power BI の公開情報や製品ブログをご確認ください。
></br>
> **公開情報** ：[管理者向けの Microsoft Fabric ドキュメント - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/admin/)
> **製品ブログ**： [Power BI ブログ — 更新とニュース | Microsoft Power BI](https://powerbi.microsoft.com/ja-jp/blog/)

---
## 目次
---
- [ライセンスについて](#ライセンスについて)
- [テナント設定](#テナント設定 )
- [ワークスペース管理](#ワークスペース管理)
- [容量の管理](#容量の管理)
- [ゲートウェイと接続の管理](#ゲートウェイと接続の管理)
- [ユーザーのアクティビティ監視](#ユーザーのアクティビティ監視)
- [PowerShellとREST API](#PowerShellとREST-API)
- [管理者監視ワークスペース](#管理者監視ワークスペース)
- [Power BI の導入時に参考する情報](#Power-BI-の導入時に参考する情報 )
- [問い合わせについて](#問い合わせについて)
- [よくある質問](#よくある質問)


</br>

---
## ライセンスについて
---
Power BIを利用するためには、無償版の Microsoft Fabric free、有償版のPower BI Pro、Power BI Premium Per Userのいずれかのライセンスが必要であり、ライセンスごとにユーザーが利用できる機能やサービスの範囲が決められます。   
ライセンスが割り当てられていないユーザーは、初回に Power BI サービスにサインインする際に、自動的に Microsoft Fabric free ライセンスが割り当てられます。 
これは、セルフサービス サインアップという機能によるライセンス割り当て方法となり、機能を無効にすることで、自動割り当てや、ユーザーがライセンスを取得すること禁止し、管理者側でライセンスの一元管理が可能になります。 

**公開情報** 
[Power BI を購入してライセンス割り当てる - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-admin-purchasing-power-bi-pro)
[Power BI サービスのライセンスの種類別機能 - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/fundamentals/service-features-license-type)
[セルフサービスの有効化と無効化の概要 - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-admin-disable-self-service)

**関連ブログ** 
[Power BI ライセンスの違い（Free・Pro・Premium Per User・Premium Per Capacity・Embedded・Fabric） | Japan CSS Support Power BI Blog (jpbap-sqlbi.github.io) ](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_license/)
[セルフサービス サインアップの無効化 | Japan CSS Support Power BI Blog (jpbap-sqlbi.github.io)](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_self-service-signup/)


---
## テナント設定
---
管理者は、テナント設定を通じて組織全体の Power BI の機能やアクセス権を管理し、ユーザーが利用できる機能やデータアクセスを詳細に設定できます。たとえば、ワークスペースの作成、ゲストユーザーのアクセス、データのエクスポートを制御することが可能です。
弊社では各テナント設定に関する推奨・非推奨の指針は提供しておりませんので、組織のセキュリティポリシーや運用状況に応じて、各設定の有効・無効についてご検討ください。
![](1.png)</br>
**公開情報** 
[テナント設定について - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/admin/about-tenant-settings)
[テナント設定のインデックス - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/admin/tenant-settings-index)
</br>
---
### ワークスペース管理
---
ワークスペースは、コンテンツの整理とアクセス制御の基本単位です。
Fabric 管理者は、管理ポータルの [ワークスペース]画面から、テナント内に存在するすべてのワークスペースを管理できます。
ワークスペースの容量設定やアクセス権限の変更だけでなく、ユーザーのマイ ワークスペースへのアクセス権限の追加も可能です。
適切なワークスペース管理により、組織内のコンテンツ共有やセキュリティを強化できます。
![](2.png)<br>

**公開情報** 
[ワークスペースの管理 - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/admin/portal-workspaces)

<br>

---
### 容量の管理
---
容量とは、特定のコンテンツに対して予約された専用のリソースセットであり、信頼性の高い一貫したパフォーマンスを提供します。Fabric 管理者は管理ポータルの [容量の設定] から、契約されている容量の確認やスケーリング設定、容量管理者の設定を行うことができます。
![](3.png)

**公開情報** 
[Fabric 容量を管理する - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/admin/capacity-settings?tabs=power-bi-premium)

<br>


---
### ゲートウェイと接続の管理
---
データ ソースに接続してコンテンツを更新するには、Power BI サービスで接続情報や、ゲートウェイの設定が必要です。
Fabric 管理者は、[接続とゲートウェイの管理] で [テナント管理] をオンにすることで、テナント全体で設定されているデータソースや、構成されているゲートウェイを表示および管理できます。
これにより、組織内のデータ接続を一元管理し、セキュリティとパフォーマンスを最適化することが可能です。
![](4.png)

**公開情報** 
[オンプレミス データ ゲートウェイの管理 | Microsoft Learn](https://learn.microsoft.com/ja-jp/data-integration/gateway/service-gateway-manage)
<br>


---
### ユーザーのアクティビティ監視
---
組織が法令順守やレコード管理などの要件を満たすためには、Power BI 内で誰がどの項目に対してどのようなアクションを実行しているかを把握することが重要です。Microsoft 365 のコンプライアンス管理センターの[監査ログ]と、Power BI REST API を基盤とする Power BI アクティビティ ログを活用することで、ユーザーのアクティビティをモニタリングできます。
これらの機能を活用することで、セキュリティ リスクの早期発見や使用状況の分析が可能となり、組織のセキュリティ強化に役立つことができます。

**公開情報** 
[Microsoft Fabric でユーザー アクティビティを追跡する - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/admin/track-user-activities)
[Power BI でユーザー アクティビティを追跡する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-admin-auditing)
[操作一覧 - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/admin/operation-list)


**関連ブログ** 
[Power BI のユーザーアクティビティ追跡方法の比較 | Japan CSS Support Power BI Blog (jpbap-sqlbi.github.io)](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_activity_log_usage_metrics/)
[ユーザーの操作におけるPower BIのアクティビティログ | Japan CSS Support Power BI Blog (jpbap-sqlbi.github.io)](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_track_activity_log/)
<br>

---
### PowerShellとREST API
---
PowerShell コマンドレットや REST API を使用することで、管理タスクの自動化やカスタム スクリプトの作成が可能です。
これにより、容量とワークスペースの管理、ユーザー権限の制御、コンテンツの棚卸しなどを効率的に行えます。
自動化スクリプトを活用することで、手動操作によるミスを減らし、管理業務の効率化を図ることができます。

**公開情報** 
[埋め込み分析と自動化のための Power BI REST API - Power BI REST API | Microsoft Learn](https://learn.microsoft.com/ja-jp/rest/api/power-bi/)
[Power BI コマンドレットリファレンス | Microsoft Learn](https://learn.microsoft.com/ja-jp/powershell/power-bi/overview?view=powerbi-ps)



**関連ブログ** 
[REST API を組み合わせて情報を取得する | Japan CSS Support Power BI Blog (jpbap-sqlbi.github.io)](https://jpbap-sqlbi.github.io/blog/powerbi/restapi/)
[セマンティック モデルの更新履歴を REST API で取得する方法 | Japan CSS Support Power BI Blog (jpbap-sqlbi.github.io)](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_refreshhistory/)
[Power BI のテナント設定の状況を一括抽出する方法 | Japan CSS Support Power BI Blog (jpbap-sqlbi.github.io)](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_api_export_tenant_settings/)
<br>

## 管理者監視ワークスペース
---
管理者監視ワークスペースは、管理者が組織向けの監視機能を活用できるように設計されています。
これを使用して、監査や使用状況の確認など、セキュリティとガバナンスのタスクを実行できます。
[管理者監視ワークスペースとは? - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/admin/monitoring-workspace)
![](5.png)<br>
> [!IMPORTANT]  
> （2024年10月31日時点）管理者監視ワークスペースは開発中のプレビュー機能であり、今後、予告なく変更または削除される可能性があります。

機能の使用状況と導入レポートは、Microsoft Fabric テナントのさまざまな機能の使用状況と導入に関する詳細な分析を提供します。
[機能の使用状況と導入レポート - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/admin/feature-usage-adoption)
![](6.png)<br>
Microsoft Purview ハブは、ファブリックのデータ資産を管理するための一元的なページです。機密データや承認状況の分析レポートを提供し、データカタログ、情報保護、データ損失防止、監査など、Purview の高度な機能へのアクセスも可能です。
[Microsoft Fabric の Microsoft Purview ハブ - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/governance/use-microsoft-purview-hub?tabs=admin-view)
![](7.png)<br>

<br>

---
### Power BI の導入時に参考する情報
---
組織全体で Power BI を正常に実装するには、慎重に検討し、計画を立てる必要があります。Power BI の導入を計画する際には、主要な考慮事項やアクション、意思決定基準、戦術的な推奨事項を以下の公開情報で詳しく説明されています。
[Power BI 実装計画 - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/guidance/powerbi-implementation-planning-introduction)
また、組織での導入後、ユーザーの Power BI 活用に役立つコンテンツを以下のブログでまとめていますので、ご活用ください。
[Power BI を学習するために役に立つコンテンツのご紹介 | Japan CSS Support Power BI Blog (jpbap-sqlbi.github.io)](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_useful_learning_link/)
<br>

---
### 問い合わせについて
---
Power BI サポート チームは、お客様が開発を進める中で発生した問題のトラブルシューティングにおいて、問題箇所に限定して 1 問 1 答 でのご支援が可能です。レポート開発、DAX 式や M クエリの作成、Embedded 環境の開発、REST API や PowerShell でのスクリプト作成等開発にかかわる内容やコンサルティングを含む内容は当リアクティブ サポート範囲外となります。
原因追及の可否については、ご利用されているサポート契約に基づきます。
※Power BI Desktop のサポートにお問い合わせいただいた場合、アプリケーションを最新バージョンにアップグレードするように求められます。

**関連ブログ** 
[Power BI のお問い合わせについて | Japan CSS Support Power BI Blog (jpbap-sqlbi.github.io)](https://jpbap-sqlbi.github.io/blog/powerbi/support_boundary/)
[Power BI の開発支援・コンサルティングを含む内容に関するお問い合わせについて | Japan CSS Support Power BI Blog (jpbap-sqlbi.github.io)](https://jpbap-sqlbi.github.io/blog/powerbi/support_boundary2/)
[Power BI サポートチームへのお問い合わせ時に気をつけるポイント | Japan CSS Support Power BI Blog (jpbap-sqlbi.github.io)](https://jpbap-sqlbi.github.io/blog/powerbi/creating_sr/)

<br>

---
### よくある質問
---
Power BI でよくある質問の公開情報や、一部公開情報にない質問をまとめてみました。
ユーザー様から質問を受けた際にご活用ください。

**公開情報** 
[Power BI に関してよく寄せられる質問 - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/consumer/end-user-faq)
[Power BI カスタム視覚化に関する FAQ - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/developer/visuals/power-bi-custom-visuals-faq)
[カスタム ビジュアル ライセンス管理と取引可能性についてよく寄せられる質問 - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/developer/visuals/licensing-faq)
[オンプレミス データ ゲートウェイに関するよく寄せられる質問 (FAQ) - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/connect-data/service-gateway-power-bi-faq)
[Power BI Premium のよく寄せられる質問 - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-premium-faq)

**関連ブログ** 
[Power BI ライセンスに関するよくある質問(FAQ) | Japan CSS Support Power BI Blog](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_license_faq/)


**その他よくある質問** 
<br>
---

**Q. マイ ワークスペースを利用させない方法はありますか？**  
**A.** マイ ワークスペースはすべての Power BI ユーザーが使用可能であるため、現在のところ制限する方法はありません。

---

**Q. Power BI Desktop の利用を制限できますか？**  
**A.** Power BI 製品自体には、直接的に Power BI Desktop の利用を制限する機能はありません。

---

**Q. 特定のコネクタをユーザーに利用させない方法はありますか？**  
**A.** 現在、特定のコネクタの利用をユーザーに対して制限する機能は提供されていません。

---

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。
<br>

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)