---
title: ワークスペースの使用量を確認する
date: 2024-02-29 00:00:00 
tags:
  - Power BI
  - Power BI サービス
  - ワークスペース
  - ストレージ
---

こんにちは、Power BI サポート チーム 丸山です。

[Power BI Pro のワークスペース容量について](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_storage/)では、組織で使用できるワークスペースのストレージ容量の考え方をご説明しました。そのうえで、「いま現在、テナント全体でどれくらいのストレージを使用しているか確認したい」というお問い合わせをよくいただきます。今回はその方法をご紹介します。

<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
## 目次
---
 [確認方法](#確認方法)
 [補足](#補足)

---
## 確認方法
---
Power BI サービスでは、残念ながら、テナント全体のワークスペースのストレージ使用容量を一括で確認できるメニューが現状ないため、各ワークスペースのストレージ使用量をそれぞれのワークスペース画面で確認するという方法になります。

具体的には以下の画面です。

Power BI サービス > 各ワークスペースの画面 > ワークスペースの設定 > システム ストレージ
<div align="center">
<img src="1.jpg">
</div>

</br>
</br>
実際のお問い合わせでは、テナント全体で現在どれだけの容量を使用しているか知りたい、というご要望を多くいただきますが、この場合は、お手数おかけしまして恐縮ですが、各ワークスペースごとに確認されたストレージ容量を足し合わせることでご確認いただけますと幸いです。

</br>
</br>

---
## 補足
---
Premium 容量ををご利用の場合は、Microsoft Fabric Capacity Metrics アプリで、各セマンティックモデルの ”Item Size” を確認することができます（下記画像）。しかしながら、この”Item Size”は前述のストレージ管理で表示されるセマンティックモデルのサイズとは一致しません。

<div align="center">
<img src="2.png">
</div>

// 公開情報：[Microsoft Fabric Capacity Metrics アプリとは? - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/fabric/enterprise/metrics-app)


理由としては以下2点です。

1. Power BI サービスではデータを取り込んでから圧縮するため、セマンティックモデルのサイズが小さくなります。一方で、メトリックアプリではこのプロセスに必要な最大メモリ量を示します。

2. インポートモードのデータ更新では、更新操作が完了するまではセマンティックモデルのスナップショットがPower BIサービスのメモリに保持されるため、必要なメモリ量はデータセットの2倍の容量が使われる可能性があります。

// 公開情報：[Power BI でのデータの更新 - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/connect-data/refresh-data#semantic-models-in-import-mode)
<div align="center">
<img src="3.png">
</div>
</br>

</br>

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。


---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)