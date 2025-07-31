---
title: Power BI データマートの廃止と Fabric Data Warehouse への移行について
date: 2025-07-31 00:00:00 
tags:
  - Power BI サービス
  - Power BI Service
  - データマート
  - Datamart
---

こんにちは、Power BI サポート チームの呂です。 
Power BI データマートが 2025 年 10 月 1 日に廃止され、Microsoft Fabric Data Warehouse（以下、Fabric DW）へ統合されます。機能廃止により、保存されたデータやレポートが失われる可能性があるため 、ご利用中のお客様は、移行計画を立てることが重要です。本記事では Microsoft 公式ドキュメントに基づき、その背景と影響、移行手順、およびよくある質問（FAQ）について解説します。 

> [!TIP]
> 公式ブログ：[Power BI Blog – Unify Datamart with Fabric Data Warehouse!](https://powerbi.microsoft.com/ja-jp/blog/unify-datamart-with-fabric-data-warehouse/)

### データマート廃止の背景
Power BI データマートは 2022 年 5 月に Power BI Premium のパブリック プレビューとして登場し、セルフサービス型のデータ分析とモデリングの新たな選択肢として活用されてきました。 
[datamarts の概要 - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/transform-model/datamarts/datamarts-overview)
[Power BI データフローとデータセット及びデータマートの紹介と比較 | Japan CSS Support Power BI Blog](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_dataflow_dataset/)

その後、Microsoft Fabric の登場により、より高度なエンタープライズ機能とスケーラビリティを備えた Fabric DW が 2024 年に一般提供（GA）されました。
[Microsoft Fabric のデータ ウェアハウスとは？ - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/data-warehouse/data-warehousing)

Fabric DW は OneLake と Delta Parquet を基盤とし、フル T-SQL 対応、Git 連携、列レベル セキュリティ、Copilot 支援など、より包括的で拡張性の高いデータ基盤を提供します。このような進化に伴い、Power BI データマートは 2025 年 10 月 1 日をもってサービスを終了し、Fabric DW へと統合されることになりました。これにより、今後は Fabric を中心としたより強力なデータ活用が可能になります。
</br>

### 移行スケジュールと影響
2025 年 6 月 1 日以降、Power BI ポータルで新しくデータマートを作成することができなくなり、代わりに Fabric DW 作成への案内が表示されます。
2025 年 10 月 1 日午前 0 時（UTC）以降、既存のデータマートは廃止となり、ワークスペースから削除されます。
**重要**：2025 年 10 月 1 日以降、データマートに保存されているデータや関連レポートへアクセスできなくなるため、事前に移行作業を行う必要があります。
</br>

### 現状の確認と影響の洗い出し
以下の方法を用いることで、テナント内のデータマートの現状を把握し、影響範囲を明確化できます。

■ Power BI 管理者向け REST API
Power BI 管理者向けの REST API を使用することで、テナント内のデータマート一覧を取得できます。
「Items - List Items」エンドポイントで type=Datamart を指定することで、データマートの作成者や最終更新日などの情報を確認できます。
詳細は、以下の公式ドキュメントをご参照ください。
[Admin - REST API (Power BI Power BI REST APIs) | Microsoft Learn](https://learn.microsoft.com/ja-jp/rest/api/power-bi/admin)

■ 管理ポータルの[ワークスペース管理]
Power BI サービスの管理ポータルでは、各ワークスペースにおけるデータマートの作成状況や構成を確認できます。
詳細は、以下の公式ドキュメントをご参照ください。
[Admin - REST API (Power BI Power BI REST APIs) | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/transform-model/datamarts/datamarts-administration)
<div align="left">
<img src="1.png">
</div>

■ Microsoft Purview Hub によるガバナンス管理
Purview Hub を使用することで、データ資産の分類、アクセス状況、依存関係などを可視化できます。データマートを含むデータ資産の利用状況をガバナンスの観点から把握するのに有効です。
詳細は、以下の公式ドキュメントをご参照ください。
[Microsoft Fabric の Microsoft Purview ハブ - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/governance/use-microsoft-purview-hub?tabs=overview)
<div align="left">
<img src="2.png">
</div>

■ Fabric 管理ポータルの使用状況レポート
Fabric 管理者は、管理ポータルの「機能の使用状況と導入」レポートを通じて、データマートを含む各種機能の利用状況を確認できます。
詳細は、以下の公式ドキュメントをご参照ください。
[機能の使用状況と導入レポート - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/admin/feature-usage-adoption)
</br>

### ウェアハウスに移行する手順
既存のデータマートを Fabric DW にアップグレードするには、次の 2 つの方法があります：
**重要**：Fabric DWを作成するには、P SKU または F SKU の容量が必要です。
1. Microsoft Learn のガイドに従って、データマートを手動で移行できます。詳細は以下の公式ドキュメントをご参照ください。
[Power BI Datamart をウェアハウスにアップグレードする方法 - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/data-warehouse/datamart-upgrade-to-warehouse#manual-upgrade-steps)

2. fabric-toolbox にて提供されているツールを活用すると、スキーマ作成とデータ移行が段階的に実施可能です。
[fabric-toolbox · GitHub](https://github.com/microsoft/fabric-toolbox/tree/main/accelerators/power-bi-to-fabric-data-warehouse-modernization)

**注意**：弊サポートチームでは、本ツールを使用したデータマートから Fabric への全体的な移行プロセスに対する包括的な支援やコンサルティングは行っておりません。スクリプト内の個別の Power BI コマンドや API を単体で実行した際にエラーが発生した場合には、コマンドや API 単位でのトラブルシューティング支援は可能です。
</br>

### よくある質問（FAQ）
**Q1. データマートが廃止されたら、保存されているデータはどうなりますか？**
A. 2025 年 10 月 1 日以降、データマート内のデータは完全に削除され、アクセスできなくなります。
**Q2. Fabric DW のサポート体制は？**
A. Fabric DW は Power BI のサポート範囲外となり、 Fabric DW の専任サポート チームが対応します。

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)