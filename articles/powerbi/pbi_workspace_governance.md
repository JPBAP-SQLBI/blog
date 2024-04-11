---
title: Power BIワークスペースのガバナンス
date: 2023-08-31 00:00:00 
tags:
  - Power BI
  - Power BI サービス
  - ワークスペース
  - ガバナンス
---

こんにちは、Power BI サポート チームの呂です。

Power BI管理者は、 [管理ポータル]からテナントに存在するワークスペースの容量やアクセス設定を変更できること、皆さんご存知かと思います。一方で、データセットの更新エラーの修正、機密データへのアクセスの制御、ユーザーが組織を離れるときのコンテンツ引き継ぎ、データ使用量の制御や、会社のポリシーとの従業員のコンプライアンスの確保などのために、[マイワークスペース]へのアクセスが必要になる場合があります。
この場合、Power BI管理者がユーザーのマイワークスペースにアクセスする機能を使用することで、マイワークスペースのガバナンスを実現可能です。この記事では、その手順ついて詳しく説明します。


<!-- more -->
> [!IMPORTANT]  
> 本記事編集時点と実際の機能に相違がある場合がございます。予めご了承ください。
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。
</br>
</br>

---
## Power BI管理者がマイワークスペースにアクセスする手順
---

マイワークスペースのアクセス権限を取得する方法は、基本的には共有ワークスペースの方法と同じです。
１．Power BIサービスで[設定]＞[管理ポータル]＞[ワークスペース]を選択します。
<div align="left">
<img src="1.png">
</div>

２．必要に応じて、ワークスペース名を絞り込みます。
※マイワークスペースの[名前]は、「PersonalWorkspace ユーザー名」で、[型]は「個人用グループ」です
<div align="left">
<img src="2.png">
</div>

３．[︙]（アクション）＞[アクセスの許可]を選択します。
<div align="left">
<img src="3.png">
</div>

※選択後、「アクセス権が正常に取得されました」との通知が表示されます
<div align="left">
<img src="4.png">
</div>

４．アクセス権限の取得後、マイワークスペースは[ユーザー名]の名前で、ワークスペース一覧で表示されるようになります。
アクセス権限を取得したマイワークスペースにアクセスいただき、必要に応じて中身のコンテンツの削除や修正、別のワークスペースへの移動などの操作をすることが可能となります
<div align="left">
<img src="5.png">
</div>

</br>

---
## 注意事項
---

・マイワークスペースへのアクセス権限は 24 時間後に自動的に取り消されます。
・退職し削除されたユーザーのマイワークスペースは [削除済み] として表示され、コンテンツは 90 日間保持されます。 
・コンテンツの保持期間中、管理者はマイ ワークスペースを[復元]オプションを利用できます。
<div align="left">
<img src="6.png">
</div>

</br>

---
### 参考情報
---
-  [Microsoft Power BI Blog：Announcing My workspace governance improvement](https://powerbi.microsoft.com/en-us/blog/announcing-my-workspace-governance-improvement-public-preview/)
-  [公開情報：ワークスペースを管理する](https://learn.microsoft.com/ja-jp/power-bi/admin/service-admin-portal-workspaces)
-  [公開情報：自分のワークスペースのガバナンスを改善する](https://learn.microsoft.com/ja-jp/power-platform-release-plan/2022wave2/power-bi/improve-my-workspace-governance)

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)