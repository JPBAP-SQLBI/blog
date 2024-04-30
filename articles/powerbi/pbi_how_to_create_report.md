---
title: Power BIでデータに接続しレポートを作成・共有する手順
date: 2024-04-30 00:00:00 
tags:
  - Power BI
  - Power BI サービス
  - Power BI Desktop
  - レポート
---


こんにちは、Power BI サポート チーム 金沢です。  
サポートチームではこれまでお客様から多くいただくお問い合わせをもとに、技術ブログ記事を投稿してきましたが、あらためて Power BI をこれから使ってみたい！という方に向けて、データに接続するところから、レポートを作成し共有するまでの一連の流れをご案内いたします。すでに多くの公開情報が用意されているため、この記事では各ステップで関連する公開情報へのリンクを載せてあります。

<!-- more -->

> [!IMPORTANT]  
> 本記事は弊社公式ドキュメントの公開情報を元に構成しておりますが、
> 本記事編集時点と実際の機能に相違がある場合がございます。  
> 最新情報につきましては、参考情報として記載しておりますドキュメントをご確認ください。

---
## 目次
---
- [目次](#目次)
- [1.	Power BIを使ってレポートを作成・共有するメリット](#1power-biを使ってレポートを作成共有するメリット)
- [2. Power BI Desktopでレポートを作成する](#2-power-bi-desktopでレポートを作成する)
  - [2-1. Power BI Desktopをダウンロードする](#2-1-power-bi-desktopをダウンロードする)
  - [2-2.	データに接続する](#2-2データに接続する)
  - [2-3.	データを加工する](#2-3データを加工する)
  - [2-4.	ビジュアル化する](#2-4ビジュアル化する)
  - [2-5.	レポートを発行する](#2-5レポートを発行する)
- [3. Power BIサービスでレポートを共有する](#3-power-biサービスでレポートを共有する)
  - [3-1.	共有に必要なライセンス](#3-1共有に必要なライセンス)
  - [3-2.	共有方法の種類](#3-2共有方法の種類)

---
## 1.	Power BIを使ってレポートを作成・共有するメリット
---

企業におけるデータの可視化・意思決定において、かつては、データをダウンロードしてExcel等に貼り付けてグラフ化し、Power Pointで資料を作成して会議やメール等で共有する流れが一般的だったかもしれません。しかしながらこのやり方ではデータが更新されるたびにデータを取得し直し、修正したグラフを張りなおす必要があります。
Power BIを使用すれば、データを連携させることで常に最新のデータがグラフに反映され、レポートをWeb上で簡単に共有することができます。


<div align="center">
<img src="従来とPowerBIの比較.png">
図：データを意思決定に活用する流れについての従来の方法とPower BIを使用する方法の比較
</div>

次の章では、Power BI Desktopでレポートを作成する方法について説明します。

---
## 2. Power BI Desktopでレポートを作成する
---

この章ではPower BI Desktopをダウンロードし、データに接続してデータを加工し、グラフ化してレポートを作成する方法を説明します。

---
### 2-1. Power BI Desktopをダウンロードする


Power BI Desktopは無料でダウンロードできるアプリケーションで、Microsoftストアからアプリを入手する方法と実行可能ファイルをコンピューターにインストールする方法があります。2つのダウンロード方法の主な違いは以下の通りです。

|  | Microsoftストアからアプリを入手 | 実行可能ファイルをコンピューターにインストール |
| --- | --- | --- |
| 自動更新 | 〇 |  |
| インストールに管理者権限が必要 |  | 〇 |
<div align=center>
表：Power BI Desktop入手方法の比較
</div>

>[!NOTE]
> 参考情報：[Power BI Desktopの取得](https://learn.microsoft.com/ja-jp/power-bi/fundamentals/desktop-get-the-desktop)


---
### 2-2.	データに接続する


Power BIではExcelファイルやSQLサーバーを始めとした様々なデータソースとの接続が可能です。対応しているデータソースとデータソースに接続する方法は以下の公開情報に記載があります。

> [!NOTE]
> 参考情報 (1)：[データ ソース](https://learn.microsoft.com/ja-jp/power-bi/connect-data/desktop-data-sources#data-sources)
> 参考情報 (2)：[クイック スタート: Power BI Desktop でデータに接続する](https://learn.microsoft.com/ja-jp/power-bi/connect-data/desktop-quickstart-connect-to-data)

---
### 2-3.	データを加工する


データソースに接続したら、データを加工します。この節ではデータを加工する方法として、データの変換と整形、リレーションシップ、計算の作成の3つを紹介します。
データの変換と整形とは、Power BI Desktop内にあるPower Queryエディターを使用して、データをフィルターしたりデータの型を設定したりすることでデータを抽出・変換ことを指します。データソースへ接続したら、最初にPower Queryエディターでデータを変換・整形することで、次以降のリレーションシップの作成や計算の際の作業負荷が小さくなります。Power Queryエディターでのデータの変換・整形方法については以下の公開情報に詳細が記述されています。

> [!NOTE]
> 参考情報：[Power BI Desktop で一般的なクエリ タスクを実行する](https://learn.microsoft.com/ja-jp/power-bi/transform-model/desktop-common-query-tasks)

リレーションシップとは、データテーブル同士を紐づけることを指し、リレーションシップで接続されたテーブルは1つのテーブルのように扱うことができます。Power BI Desktopではリレーションシップを自動的に作成しますが、手動で調整することもできます。リレーションシップの作成と管理については以下の公開情報に詳細が記述されています。

> [!NOTE]
> 参考情報：[Power BI Desktop でのリレーションシップの作成と管理](https://learn.microsoft.com/ja-jp/power-bi/transform-model/desktop-create-and-manage-relationships)

計算とは、例えば単価と販売数を掛け算して販売金額を算出するように、データに関数や演算子を使用して分析することを指します。Power BIにはM数式言語とDAXと呼ばれる言語がありますが、簡易にレポートを作成するのであればDAXを使用することをおすすめします。DAXについての基本的な概念を説明した公開情報は以下をご参照ください。

> [!NOTE]
> 参考情報：[Power BI Desktop における DAX の基本を学習する](https://learn.microsoft.com/ja-jp/power-bi/transform-model/desktop-quickstart-learn-dax-basics)

---
### 2-4.	ビジュアル化する


データを加工したら、いよいよグラフや図を作成します。Power BIには基本的な棒グラフや折れ線グラフだけでなく塗分け地図やQ&Aを設定することが可能です。現在Power BIで使用可能なビジュアルについては以下の公開情報をご参照ください。

> [!NOTE]
> 参考情報：[Power BI での視覚化の種類](https://learn.microsoft.com/ja-jp/power-bi/visuals/power-bi-visualization-types-for-reports-and-q-and-a)

---
### 2-5.	レポートを発行する


これまでの節で作成したレポートは、次の章で公開するためにPower BIサービス上に発行する必要があります。発行するには、Power BI Desktopでサインインして発行先を選択します。発行先とはワークスペースと呼ばれる、特定のコンテンツで同僚と共同作業を行う場所のことを指しています。発行の操作方法とワークスぺースの詳細は以下のリンクで説明されています。

> [!NOTE]
> 参考情報 (1)：[Power BI Desktop からセマンティック モデルとレポートを発行する](https://learn.microsoft.com/ja-jp/power-bi/create-reports/desktop-upload-desktop-files)
> 参考情報 (2)：[ワークスペースで共同作業する](https://learn.microsoft.com/ja-jp/power-bi/consumer/end-user-workspaces)


---
## 3. Power BIサービスでレポートを共有する
---

第2章までの操作でレポートを作成してワークスペースへ発行しました。第3章ではレポートを含めたコンテンツをPower BIサービスで共有する方法について、既存のBlog記事を紹介します。

---
### 3-1.	共有に必要なライセンス


コンテンツを共有するにあたって必要なライセンスについてはこちらの記事をご覧ください。

> [!NOTE]
> 参考情報：[Power BI ライセンスの違い（Free・Pro・Premium Per User・Premium Per Capacity・Embedded・Fabric）](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_license/)

---
### 3-2.	共有方法の種類


コンテンツの共有方法についてはこちらの記事をご覧ください。

> [!NOTE]
> 参考情報：[Power BI サービスでのコンテンツ共有方法の種類](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_contents_share_1/)

以上、本ブログが少しでも皆様のお役に立てますと幸いでございます。

---

**アンケートご協力のお願い**
Japan CSS Support Power BI Blog では、作成する記事やブログの品質向上を目的に、匿名回答でのアンケートを実施しております。
ユーザー様のご意見・ご要望を参考に今後もお役に立てるブログを目指してまいりますので、ぜひご協力いただけますと幸いでございます。 

※　所要時間は1分程度となります。
[【ご協力のお願い】Microsoft Japan CSS Power BI Blog ご利用に関するアンケート](https://jpbap-sqlbi.github.io/blog/powerbi/pbi_blogsurvey2022/)