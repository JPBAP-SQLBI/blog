---
title: 組織内のユーザーのマイ ワークスペースへアクセスする方法
date: 2023-02-28 00:00:00 
tags:
  - Power BI
  - Power BI サービス
  - Power BI Service
  - ワークスペース
  - マイ ワークスペース
  - workspace
  - My workspace
---

こんにちは、Power BI サポート チームのファムです。

組織内のユーザーが退職やプロジェクト離任時に、そのユーザーのマイ ワークスペースで作成されたレポートやデータセットにアクセスしたい場面がございませんでしょうか。実は、Power BI管理者権限のユーザーなら、組織内のユーザーのマイ ワークスペースへ適用するごとに24時間限定でアクセスできる機能がございます。

本ブログでは、Power BI 管理者権限で組織内のユーザーのマイ ワークスペースへアクセスする方法の手順をご紹介します。


<!-- more -->
> [!IMPORTANT]  
> ご紹介する機能は、現時点ではプレビュー機能で開発段階のため、今後予告なしに機能が削除されたり、または動作変更が発生する可能性があったりしますので、あらかじめご了承ください。
> 本記事編集時点と実際の機能に相違がある場合がございます。予めご了承ください。
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。
</br>

---
## 目次
---
1. [マイ ワークスペースとは](#マイ-ワークスペースとは)
2. [組織内のユーザーのマイ ワークスペースへアクセスする手順](#組織内のユーザーのマイ-ワークスペースへアクセスする手順)
</br>

---
##  マイ ワークスペースとは
---
すべての Power BI ユーザーには、マイ ワークスペースと呼ばれる個人用ワークスペースがあり、ユーザーはそこで自分のコンテンツを操作できます。 通常、マイ ワークスペースにアクセスできるのはそのマイ ワークスペースの所有者のみですが、Power BI 管理者は一連の機能を使用して、それらのワークスペースを管理できます。

> **参考情報**
>  [マイ ワークスペースを管理する](https://learn.microsoft.com/ja-jp/power-bi/admin/service-admin-portal-workspaces#gain-access-to-any-users-my-workspace)
> ※本情報の内容（添付文書、リンク先などを含む）は作成日時点でのものであり、予告なく変更される場合があります。


---
##  組織内のユーザーのマイ ワークスペースへアクセスする手順
---

Power BI管理者権限のユーザーで、Power BIサービスにサインイン後、「**…**」＞ 「**設定**」＞ 「**管理ポータル**」＞ 「**ワークスペース**」へ移動します。

ユーザーのマイ ワークスペースの確認方法は、ワークスペースの名前が「**PersonalWorkspace ＋ ユーザー名**」となっているか、またはワークスペースの型が「**個人用グループアクティブ**」となっていることを確認します。

<div align="center">
<img src="image1.png">
</div>

アクセスしたいユーザーのマイ ワークスペースを選択し、「**アクセスの取得**」を押下します。その時点で、該当のユーザーのマイ ワークスペースにアクセスできます。
※「アクセスの取得」ボタンを押下した時点から24時間後に、アクセス権限が自動的に解除されます。
<div align="center">
<img src="image2.png">
</div>

管理者の「**ワークスペース**」から、該当のユーザーのマイ ワークスペースを確認できます。
<div align="center">
<img src="image3.png">
</div>

該当ユーザーの「**マイ ワークスペース**」にアクセスし、ワークスペース内のコンテンツを確認できます。
<div align="center">
<img src="image4.png">
</div>

マイ ワークスペースのレポートやデータセットの閲覧、.pbixファイルのダウンロードなどを行うことも可能です。
<div align="center">
<img src="image5.png">
</div>


以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)