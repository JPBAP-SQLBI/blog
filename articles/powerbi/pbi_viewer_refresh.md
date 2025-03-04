---
title: 閲覧者がセマンティックモデルを更新する方法について
date: 2025-02-28 00:00:00 
tags:
  - Power BI
  - Power BI Service
  - Power BI Power Automate Visual
  - Power BI サービス
  - Power BI Power Automate ビジュアル
  - semantic model refresh
  - セマンティックモデルの更新
  - Viewer refresh
  - 閲覧者で更新
  
---
こんにちは、Power BI サポート チームのクルボノブです。

通常、Power BI レポートのデータは、セマンティック モデルの所有者によって設定されたスケジュール更新、またはオンデマンド更新によって最新の状態に保たれます。どちらの方法も、基本的にはセマンティック モデルの所有者が実行する必要があります。

しかし、セマンティック モデルの所有者ではなく、また所有権を引き継ぐこともできない閲覧者権限のユーザーが、レポートを最新のデータに更新したいというケースも多くあります。
本記事では、Power Automate ビジュアルのフローを使用して、閲覧者権限のユーザーがセマンティック モデルの所有者を介さずにレポートを更新できる方法をご紹介します。



---
## 前提条件と制限事項
---
•	Power BI Pro/Premium Per User ライセンス（セマンティックモデルの所有者）
•	更新対象のセマンティック モデルの所有者が設定したレポート
•	Power BI Desktop（更新を実行するPower Automate ビジュアルの追加/編集に必要）


---
## 手順
---
### １．PBIX ファイルのダウンロード
Power Automate ビジュアルのフローでは、更新対象のセマンティック モデルとワークスペースを指定する必要があるため、Power BI Desktop の初回レポート作成段階で閲覧者の更新を設定することはできません。そのため、レポートのpbixファイルをダウンロードします。
1.	一度レポートを Power BI サービスに発行します。
2.	「レポートとデータのコピー (.pbix)」を選択し、PBIX ファイルをダウンロードします。

<div align="center">
<img src="1.png">
</div>   <br>  

<div align="center">
<img src="2.png">
</div>  


### ２．Power Automate ビジュアルの追加
ダウンロードしたpbixファイルを Power BI Desktop で開き、Power Automate ビジュアルを追加します

<div align="center">
<img src="3.png">
</div>  

### ３．Power Automate ビジュアルのフローを編集
追加した Power Automate ビジュアルの右上の「その他のオプション […]」＞「編集」をクリックします。

<div align="center">
<img src="4.png">
</div>  

### ４．フローの作成
フローの編集画面で、以下の手順を実施します。
1.	「+新規」＞「インスタントクラウドフロー」＞「新しいステップ」 を選択します。
2.	操作リストで 「Power BI」 を検索し、クリックします。
3.	「アクション」タブで「データセットの更新」 を選択します。

<div align="center">
<img src="5.png">
</div>    <br> 

<div align="center">
<img src="6.png">
</div>    <br> 

<div align="center">
<img src="7.png">
</div> 

### ５．ワークスペースとセマンティック モデルの設定
次の画面で、pbix ファイルをダウンロードしたワークスペースとセマンティック モデルを指定し、「保存」 をクリックします。

<div align="center">
<img src="8.png">
</div>  

### ６．更新ボタンの作成と調整
更新フローを実行する以下のボタンが作成されますので、必要に応じて名前の変更やサイズと位置の調整等を行います 。

<div align="center">
<img src="9.png">
</div>


### ７．実行ユーザーの設定
ボタン右上の「その他のオプション[…]」＞「編集」をクリックし、以下の画面でレポートを更新する閲覧者のアカウントを「実行のみのユーザー」追加します。


<div align="center">
<img src="10.png">
</div>    <br> 

<div align="center">
<img src="11.png">
</div>


### ８．レポートの再発行と動作確認

設定が完了したら、レポートを同じワークスペースに再発行し、閲覧者のアカウントでアクセスし、Power Automate ビジュアル上でフローを実行して、セマンティックモデルが 更新できることを確認します。
「更新履歴」 にて、Power Automate ビジュアルで実行した更新が 「API 経由」 として表示されます。

<div align="center">
<img src="12.png">
</div>



---
## 注意事項
---
１．	共有容量(Power BI Pro)のワークスペースの場合、過度な更新頻度が他のレポートのパフォーマンスに影響を与えます。
２．	共有容量(Power BI Pro)のワークスペースの場合、セマンティックモデルの更新数はスケジュール更新と API 更新を合わせて、1 日 最大 8 回 までです。
３．	Power BI の「更新履歴」では、Power Automate 経由の更新が「API 経由」として記録されるため、どのユーザーが実行したのかを詳細に把握しにくいです。
４．	Premium ワークスペースではより多くの更新を処理できますが、それでも 過剰な更新は避けるべきです。
５．	Power Automateビジュアルを使用する際の考慮事故と制限事項が適用されます。
> [!NOTE]
> 参考# [Power BI 用の Power Automate ビジュアルを作成する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/create-reports/power-bi-automate-visual?tabs=powerbi-desktop#considerations-and-limitations)



---
## おわりに
---
この記事では、閲覧者権限を持つユーザーがセマンティック モデルの所有者を介さずに Power BI レポートを更新できる方法についてご紹介しました。
この設定を活用することで、管理者やセマンティック モデル所有者の負担を軽減し、レポート閲覧者が必要なタイミングでオンデマンドでデータを更新できる環境を実現できます。また、セマンティック モデルの設定にアクセスすることなく最新のデータを確認できるため、運用の効率化にもつながります。
ぜひ本記事の内容をご参考に、より柔軟なレポート運用をご検討いただければ幸いです。
以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

その他のPower AutomateとPower BIの連携については以下のブログ記事でも紹介していますので併せてご確認お願いいたします。

> [!NOTE]
> 参考# [Power BI と Power Automate の連携 | Japan CSS Support Power BI Blog](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_power%20automate/)


以上、本ブログが少しでも皆さまのお役に立てますと幸いでございます。