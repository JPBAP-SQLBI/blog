---
title: Power BI アプリの紹介
date: 2022-11-30 00:00:00 
tags:
  - Power BI
  - Power BI サービス
  - Power BI アプリ
---

こんにちは、Power BI サポート チームの呂です。

レポートやダッシュボード以外のコンテンツ配布方法として、Power BI アプリという便利な機能があることをご存知でしょうか？
今回は、Power BI アプリの機能やご利用方法について紹介します。

<!-- more -->
> [!IMPORTANT]  
> 本記事編集時点と実際の機能に相違がある場合がございます。予めご了承ください。
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。
</br>

---
## 目次
---
1. [Power BI アプリとは](#Power-BI-アプリとは)
2. [ライセンス要件](#ライセンス要件)
3. [組織アプリ](#組織アプリ)
4. [テンプレートアプリ](#テンプレートアプリ)
</br>

---
## Power BI アプリとは
---

Power BI アプリはパッケージ化するコンテンツを作成し、アプリとして多くの対象ユーザーに配布できる機能です。
Power BI アプリには組織内に配布する組織アプリと、組織外の顧客に配布するテンプレートアプリという２種類があります。



---
## ライセンス要件
---

アプリを作成または更新するには、Power BI Pro または Premium Per User (PPU) のライセンスが必要です。
アプリの閲覧についてはレポートと同様に閲覧権限が必要になります。各ライセンスの閲覧可否の詳細につきましては、以下ブログをご参考ください。

参考情報
[Power BI ライセンスの違い（Free・Pro・Premium Per User・Premium Per Capacity・Embedded）― ライセンス組み合わせのコンテンツ閲覧可否](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_license/#%E3%83%A9%E3%82%A4%E3%82%BB%E3%83%B3%E3%82%B9%E7%B5%84%E3%81%BF%E5%90%88%E3%82%8F%E3%81%9B%E3%81%AE%E3%82%B3%E3%83%B3%E3%83%86%E3%83%B3%E3%83%84%E9%96%B2%E8%A6%A7%E5%8F%AF%E5%90%A6)
</br>

---
## 組織アプリ
---

組織アプリは、特定のワークスペースにあるコンテンツをバージョン管理の上パッケージ化して、組織全体または特定のユーザーに発行する機能です。 アプリはワークスペースと異なるアクセス許可を設定でき、また各対象ユーザーに対して異なるコンテンツを表示することができますため、組織内における大規模なコンテンツ配布する際に便利な機能になっています。

レポート、ダッシュボードとの機能比較

| 機能                 | レポートダッシュボード       | ダッシュボード                       | 組織アプリ
| ---------------------| ---------------------------| -----------------------------------| ---------------------------| 
| コンテンツ            | レポートのページ            | 複数のレポートに存在するビジュアル     | 同一ワークスペースにある複数レポート及びダッシュボードのコンテンツ
| アクセス              | レポート単位で設定可能      | ダッシュボード単位で設定可能           | 特定のユーザーグループに特定のコンテンツを表示可能
| コピーの保存          | 可                         | 可                                  | 不可
| ダウンロード          | 可                         | 不可                                | 不可
| 埋め込み              | 可                         | 不可                                | 可
</br>


### 組織アプリの発行方法

1. ワークスペース画面から、右上の[アプリの作成]をクリックします。
<div align="center">
<img src="1.png">
</div>

2. セットアップ画面でアプリ名と説明（必須）、ロゴの変更、連絡先などを指定できます。
設定終了後、[次へ: コンテンツを追加する]を選択します。

<div align="center">
<img src="2.png">
</div>

3. コンテンツ画面で、[コンテンツの追加]を選択します、ポップアップ画面でアプリに追加したいレポート／ダッシュボードをチェックし、[追加]を選択し、[次へ: 対象ユーザーを選択する]を選択します。

<div align="center">
<img src="3.png">
</div>

4. 対象ユーザー画面で、特定のユーザーグループに特定のコンテンツを表示させる設定を行えます。
4-①　必要に応じて[対象ユーザー]を作成します。
※作成しました対象ユーザーをダブルクリックすると名前の変更が可能です。
4-②　選択している対象ユーザーに表示／非表示したい内容を編集する。
※画面ショットの例では、営業部に所属するユーザーに、Report03／Report04／Report05のみを表示するように設定しております。
4-③　[Audience Accessを管理する]で対象ユーザー、もしくは対象ユーザーが所属しているグループのアクセス権限を設定します。

> [!TIP]
> [Audience Accessを管理する]>[詳細]で対象ユーザーへのデータセット共有やコンテンツのビルド許可の設定も可能です。

<div align="center">
<img src="4.png">
</div>

5. 以上の設定終了後、[アプリの発行]を選択すると、コンテンツは組織として発行されます。
発行後の組織アプリは、Power BIサービス左側のナビゲーションの[アプリ]一覧から確認することができます。

<div align="center">
<img src="5.png">
</div>
</br>

### 組織アプリの編集方法

アプリ発行後、ワークスペース画面右上の[アプリの作成]ボタンが[アプリの更新]に変更され、選択すると発行済のアプリの内容を編集することができます。

<div align="center">
<img src="6.png">
</div>
</br>

### 組織アプリの削除方法
ワークスペース画面＞[･･･]>[アプリ発行の取り消し]で組織アプリを削除できます。

<div align="center">
<img src="7.png">
</div>
</br>

---
## テンプレートアプリ
---

テンプレートアプリはMicrosoftまたはPower BIパートナーが顧客に向けて提供しているダッシュボードとライブデータソースのパッケージです。自身でレポートなどを構築する必要がなく、取得後にすぐに使用できます。
※Power BIパートナーは、Microsoftと提携して、BIソリューションに提供するPower BIの認定パートナーやコンサルタントのことです。
</br>

### テンプレートアプリの取得

Power BIサービス左側のナビゲーションの[アプリ]>[アプリの取得]から、テンプレートアプリを検索し、ダウンロードすることができます。

<div align="center">
<img src="8.png">
</div>

以下、例としてPower BI関連の便利なテンプレートアプリを２つご紹介します：

[■Power BI Premium Capacity Utilization and Metrics](https://appsource.microsoft.com/en-us/product/power-bi/pbi_pcmm.pbipremiumcapacitymonitoringreport)


<div align="center">
<img src="9.png">
</div>

Premium 容量管理者が、Power BI Premium Gen2 (プレビュー) ワークスペースのデータセット、レポート、データフローなどで使用されている CPU 使用率、処理時間、メモリの量を確認できるアプリです。

> [!TIP]
> 前提条件：Gen2 容量であること及び容量管理者アカウントが必要です
> 公開情報：[Premium Gen2 メトリック アプリをインストールする - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/enterprise/service-premium-install-gen2-app?tabs=1st)


[■Power BI Release Plan](https://appsource.microsoft.com/en-us/product/power-bi/pbicat.powerbi-release-plan)

Power BIでリリース済と今後リリース予定の機能を確認できるアプリです。

<div align="center">
<img src="10.png">
</div>

> [!TIP]
> 公開情報：[Power BI リリース計画レポートに接続する - Power BI | Microsoft Learn](https://learn.microsoft.com/ja-jp/power-bi/connect-data/service-connect-to-power-bi-release-plan)
</br>

### テンプレートアプリの更新

現在、テンプレートアプリの新しいバージョンがリリースされても、最新バージョンに自動で更新されません。最新バージョンを利用する場合は、以下の手順で更新してください。
１．[アプリの取得]からもう一度ご更新されたいアプリをダウンロードする。
２．既に旧バージョンをインストールしている場合、以下のポップアップが表示され、更新したいアプリを選択しインストールすると、テンプレートアプリは最新バージョンに更新されます。

<div align="center">
<img src="11.png">
</div>

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。
</br>

---
### 参考情報
---
-  [公開情報：Power BI のアプリ](https://learn.microsoft.com/ja-jp/power-bi/consumer/end-user-apps)
-  [公開情報：Power BI でアプリを発行する](https://learn.microsoft.com/ja-jp/power-bi/collaborate-share/service-create-distribute-apps)
-  [公開情報：組織でテンプレート アプリをインストールし、共有し、更新する](https://learn.microsoft.com/ja-jp/power-bi/connect-data/service-template-apps-install-distribute)
-  [公開情報：Power BI テンプレート アプリとは](https://learn.microsoft.com/ja-jp/power-bi/connect-data/service-template-apps-overview)
-  [公開情報：Power BI でテンプレート アプリを作成する](https://learn.microsoft.com/ja-jp/power-bi/connect-data/service-template-apps-create)
-  [公開情報：Power BI でダッシュボードとレポートを含むアプリをインストールして使用する](https://learn.microsoft.com/ja-jp/power-bi/consumer/end-user-app-view)
