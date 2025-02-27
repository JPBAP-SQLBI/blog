---
title: Power BI ワークスペースに関するよくあるお問い合わせ 
date: 2021-08-31 00:00:00 
tags:
  - Power BI
  - Workspace
  - ワークスペース
  - クラシックワークスペース
  - 新しいワークスペース
  - モダンワークスペース
  - Power BI サービス
  - Power BI Service
---


こんにちは、Power BI サポート チームの山本です。 

前回「[Power BI ワークスペースについて ～クラシックワークスペースと新しい(アプリ)ワークスペース～](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_workspace_classic_and_app/)」にてPower BI におけるワークスペースをご紹介しましたが、 

今回、ワークスペースについてよくお寄せいただくお問い合わせについてまとめました。 

<!-- more -->

<br>

---

### Q. 最近Teams で作ったチームがワークスペースに反映されなくなっている。

Teams で作ったチームは Microsoft 365 グループ、つまりクラシックワークスペースです。この場合テナント設定の"クラシックワークスペースの作成のブロック"が<b>"有効化"</b>されている可能性があります。ブロックを無効にすることで再表示が可能です。

<div align="center">
<img src="blog_workspace_006.png" alt="画像1_ブロック" title="画像1_ブロック">
</div>



### Q. 既存のクラシックワークスペースは新しい(アプリ)ワークスペースに変更できるのか？

クラシックワークスペースのホーム画面上部よりアップグレードを実施いただくことで可能になりました。

<div align="center">
<img src="blog_workspace_007.png" alt="画像2_アップグレードポップ" title="画像2_アップグレードポップ">
</div>


また Power BI 管理者によるワークスペースのアップグレードも可能です。
管理ポータルのワークスペースリストよりご確認いただけます。

<div align="center">
<img src="blog_workspace_008.png" alt="画像3_アップグレード設定" title="画像3_アップグレード設定">
</div>

さらに2021年7月より一括アップグレード機能がご利用いただけるようになりました。
既存のクラシックワークスペースをすべて新しい(アプリ)ワークスペースに変更することが可能です。

<div align="center">
<img src="blog_workspace_011.png" alt="画像4_アップグレード一括設定" title="画像4_アップグレード一括設定">
</div>

### Q. 新しい(アプリ)ワークスペースにアップグレードした場合、メンバーや管理権限はどうなるのか？

クラシックワークスペースに紐づいていた M365 グループの所有者は、新しい(アプリ)ワークスペースの「管理者」ロールに、M365 グループ自体は「メンバー」ロールとして構成されます。新しい(アプリ)ワークスペースはグループでのメンバー追加も可能ですので、クラシックワークスペースを利用していたユーザーはそのまま新しい(アプリ)ワークスペースを利用できることになります。M365 グループ所有者には新しい(アプリ)ワークスペースの管理権限が付与されるため、引き続きワークスペースのアクセス許可のコントロールを行うことができます。

<div align="center">
<img src="blog_workspace_009.png" alt="画像5_アップグレード後の権限" title="画像5_アップグレード後の権限">
</div>


アップグレードすることによって、M365 グループ側に変更が伴うような影響はありません。ワークスペースをアップグレードした後も M365 グループは、引き続き残ります。

アップグレードに関する詳細については、以下も合わせてご参照ください。
<span style="font-size: 80%; color: black;">参考：[Power BI でクラシック ワークスペースを新しい(アプリ)ワークスペースにアップグレードする](https://learn.microsoft.com/ja-jp/power-bi/collaborate-share/service-upgrade-workspaces)</span>

### Q. クラシックワークスペースと新しい(アプリ)ワークスペースの見分け方は？

管理ポータルのワークスペースリストに表示される「型」で見分けることが可能です。

| 型             | ワークスペースのタイプ   | 
| -------------- | ------------------------ | 
| ワークスペース | 新しい(アプリ)ワークスペース     | 
| グループ       | クラシックワークスペース | 

<div align="center">
<img src="blog_workspace_010.png" alt="画像6_種類" title="画像6_種類">
</div>


### Q. コンテンツパックはどうなるのか？

新しい(アプリ)ワークスペースではコンテンツパックは対応しておらず、2021年2月以降、新規作成と編集機能が削除され、今後コンテンツパックが削除される予定です
コンテンツパックをインストールしたワークスペース、もしくはコンテンツパック発行元のワークスペースをアップグレードすると、コンテンツパックのコピーが配置されるようになります。
事前に必要なコンテンツパックは、お早めにワークスペースのアップグレードをご検討ください。
<span style="font-size: 80%; color: black;">参考: [アップグレード中のコンテンツパック](https://learn.microsoft.com/ja-jp/power-bi/collaborate-share/service-upgrade-workspaces#content-packs-during-upgrade)</span>

</br>

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)