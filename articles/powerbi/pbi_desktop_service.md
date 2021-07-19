---
title: Power BIでレポート作成・分析を行うために必要なものは？ ~ Power BI DesktopとPower BI サービスの違い ~
date: 2021-07-21 15:00:00
tags:
  - Power BI サービス
  - Power BI Desktop
  - Power BI
---

こんにちは、Power BI サポート チームです。

「Power BI Desktop」、「Power BI サービス」、「Power BI Pro」… など色々なキーワードを耳にするけれど、それぞれの機能の違いは？BIレポートを作成するためには何が必要なの？という疑問を持つ方が多くいらっしゃるかと思います。

<!-- more -->

そこで今回は、Power BIの活用を始めるにあたり、理解しておくべきポイントについて２つにわけてご案内いたします。

1. [Power BIでレポート作成・分析を行うために必要なものは？ ~ Power BI DesktopとPower BI サービスの違い ~](./pbi_desktop_service/)
2. [作成したレポートを組織内で共有するために必要なライセンスは？~ Power BIライセンス（Free・Pro・Premium Per User・Premium Per Capacity・Embedded）の違い ~](../pbi_license/)

---
## Power BIでレポート作成・分析を行うために必要なものは？
###            ~ Power BI DesktopとPower BI サービスの違い ~
---

Power BI は、様々なデータソースを基に、データをビジュアル化したレポートを作成し分析を行うためのツールです。

レポート作成・分析を行う方法として、PCにインストールして使うアプリケーション “Power BI Desktop”とWebブラウザからサインインして使うクラウド サービス “Power BI サービス” のご用意があります。

レポート作成においては、Power BI サービスには多くの制限がありPower BI Desktopの方が機能が優れているため、多くのユーザーは「Power BI Desktopでレポートを作成したあと、Power BIサービスでレポートを他のユーザーと共有する」という使い分けをするのが一般的です。

![](./pbi_desktop_service.png)


Power BI DesktopとPower BI サービスの機能比較を一覧にすると以下の通りとなります。

| 機能  | Power BI Desktop  | Power BI サービス |
| ------------ | ------------ | ------------ |
| 多くのデータソース  | 〇  |   |
| 変換  | 〇  |   |
| 整形とモデリング  | 〇  |   |
| メジャー  | 〇  |   |
| 計算列  | 〇  |   |
| Python  | 〇  |   |
| テーマ  | 〇  |   |
| RLSの作成  | 〇  |   |
| レポート  | 〇  | 〇  |
| 視覚化  | 〇  | 〇  |
| セキュリティ  | 〇  | 〇  |
| フィルター  | 〇  | 〇  |
| ブックマーク  | 〇  | 〇  |
| Q&A  | 〇  | 〇  |
| Rビジュアル  | 〇  | 〇  |
| いくつかのデータソース  |   | 〇  |
| ダッシュボード  |   | 〇  |
| アプリとワークスペース  |   | 〇  |
| 共有  |   | 〇  |
| データフローの作成  |   | 〇  |
| ページ分割されたレポート  |   | 〇  |
| RLS管理  |   | 〇  |
| ゲートウェイ接続  |   | 〇  |


Power BI DesktopとPower BI サービスについて、それぞれもう少し詳細にご案内いたします。

---
## Power BI Desktopとは？
---

Power BI Desktopは、ライセンスの有無に関わらず、誰でも無償でPCにインストールして使用することができるアプリケーションです。

Windows 10 OS (LTSB/LTSCは除く) はMicrosoft Storeからストア アプリとしてインストールすることも可能です。

Power BI DesktopでPower BIのライセンス（Free、ProまたはPremium Per User）が必要となるタイミングとしては、Power BIサービス上のデータセットやデータフローからデータを取得するとき、または作成したレポートをPower BIサービス上に発行するときなど、Power BI サービスと接続を行うときのみであり、レポート作成においてライセンスによる機能差はありません。

上記のようなPower BI サービスとの接続が不要な場合は、サインインする必要はありません。

つまり、ライセンスがなくても使用できます。

> **参考情報**
> Power BI Desktopの取得方法や最小要件についてご案内しています。
> - [Power BI Desktop の取得](https://docs.microsoft.com/ja-jp/power-bi/fundamentals/desktop-get-the-desktop)
> - [ダウンロード センター Power BI Desktop](https://www.microsoft.com/ja-jp/download/details.aspx?id=58494)

---
## Power BI サービスとは？
---

Power BI サービス (app.powerbi.com) は、Webブラウザ上でサインインすることで、Azure上でPower BIを使用することができる SaaS (サービスとしてのソフトウェア) の一部です。

レポート、ダッシュボードの作成、アプリ、ワークスペースの使用、コンテンツの共有など、組織内での共同作業において便利な機能のご用意がありますが、所持しているライセンスによって、使用できる機能が異なっていきます。

Power BI ライセンスについては、以下ブログで引き続きご案内いたします。

- [作成したレポートを組織内で共有するために必要なライセンスは？~ Power BIライセンス（Free・Pro・Premium Per User・Premium Per Capacity・Embedded）の違い ~](../pbi_license/)

> **参考情報**
> 上記内容については、以下公開情報をもとにまとめています。
> ぜひ本ブログとあわせてご覧ください。
> - [Power BI Desktop と Power BI サービスの比較](https://docs.microsoft.com/ja-jp/power-bi/fundamentals/service-service-vs-desktop)
> - [Power BI Desktop とは何ですか?](https://docs.microsoft.com/ja-jp/power-bi/fundamentals/desktop-what-is-desktop)
> - [Power BI サービスとは何ですか? ](https://docs.microsoft.com/ja-jp/power-bi/fundamentals/power-bi-service-overview)

以上、本Blogが少しでも皆様のお役に立てますと幸いでございます。

---

**本ブログの関連記事**
- [作成したレポートを組織内で共有するために必要なライセンスは？~ Power BIライセンス（Free・Pro・Premium Per User・Premium Per Capacity・Embedded）の違い ~](../pbi_license/)







