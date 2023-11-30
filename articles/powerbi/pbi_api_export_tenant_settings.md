---
title: Power BI のテナント設定の状況を一括抽出する方法
date: 2023-11-30 00:00:00 
tags:
  - Power BI
  - Power BI サービス
  - テナント設定
---


こんにちは、Power BI サポート チーム 丸山です。

Power BI を管理していくうえで、テナント設定が今どのような設定状況になっているか、一覧で把握したいというお問い合わせをいただくことがございます。その場合、すべての設定項目を管理ポータルのテナント設定で目視の確認をするには工数がかかりますが、APIを利用する ことで一覧を簡単に抽出することができます。今回はその具体的な方法をご紹介します 。

<!-- more -->
<div align="center">
<img src="1.png">
</div>

</br>

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
## 目次
---
 [概要と前提条件](#概要と前提条件)
 [手順](#手順)
 [ユースケース](#ユースケース)

---
## 概要と前提条件
---
REST API の Get Tenant Settings は、テナント設定の全設定状況を 1 つの JSON 応答で返します。

// 公開情報：[Tenants - Get Tenant Settings - REST API (Admin) | Microsoft Learn](https://learn.microsoft.com/en-us/rest/api/fabric/admin/tenants/get-tenant-settings?tabs=HTTP)

この REST API を実行するには、Office 365 グローバル管理者か Fabric 管理者の権限を持っているか、サービス プリンシパルを使用して認証する必要があります。また、Tenant.Read.All または Tenant.ReadWrite.All スコープも必要です。

</br>

---
## 手順
---

具体的な手順は以下です。

1. Tenants - Get Tenant Settings のページにアクセスをします。

// 公開情報：[Tenants - Get Tenant Settings - REST API (Admin) | Microsoft Learn](https://learn.microsoft.com/en-us/rest/api/fabric/admin/tenants/get-tenant-settings?tabs=HTTP)

2. 「Try it」 を押下します。
<div align="center">
<img src="2.png">
</div>
 
</br>

3. 実行する管理者アカウントでサインインします。
①「新しいソース」 > 「その他」
<div align="center">
<img src="3.png">
</div>

</br>

4. パラメータなどは特に編集する必要はなく、下部の「Run」 押下します。

<div align="center">
<img src="4.png">
</div>

</br>

5. 結果が返ります。各項目の意味は以下のとおりです。

<div align="center">
<img src="5.png">
</div>

</br>

---
## ユースケース
---

よくあるお問い合わせのシナリオから、本記事で紹介した機能のユースケースをいくつか箇条書きでご紹介いたします。同じご要望がある場合、ご参考にしていただけますと幸いです。
</br>
•	現在 の構成を設定状況から文書化する
•	管理者以外のユーザーとテナント設定の状況を共有する
•	さまざまな環境 (開発、テスト、運用など) のテナント設定の比較する
•	テナント設定の変更履歴を保存して、必要に応じて追跡する
•	etc

 

</br>

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

</br>

> [!NOTE]
> // 公開情報：[Tenants - Get Tenant Settings - REST API (Admin) | Microsoft Learn](https://learn.microsoft.com/en-us/rest/api/fabric/admin/tenants/get-tenant-settings?tabs=HTTP)

</br>

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)